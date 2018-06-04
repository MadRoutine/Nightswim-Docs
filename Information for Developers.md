# Information for Developers
Nightswim is written in JavaScript, according to the ECMAScript 6/ECMAScript 2015 specification. It utilizes ES6 modules. Webpack is used for packaging, transpiling (with Babel) and minifying (with Uglifyjs).

I follow some of JSLint.com's recommendations, like using double quotes, ending every statement with a semicolon, and avoiding for-loops and ++/-- iterators. I do use `this`, `instanceof`, and ES6 classes.

## src/main.js
Main.js is the entry point of the program. It starts execution on the document.onload event, near the bottom of the file. The only thing that will really happen at that point is the call to `initstory()`. This function will download the gamedata through four AJAX-requests (for respectively init.json, locations.json, npc_list.json and obj_list.json). When obtained, alle Javascript objects will be instantiated.

Once the player clicks "Let's go" the audio will be initialized and the audio for the start location will start playing (unless sound is muted). This has to happen right here, because Safari and Chrome policies require sound playback by direct user interaction. All the other stuff to setup the story will happen in `startStory()`. Once that has run, we'll head into the heart of the program: `enterLocation(locID)`.

### enterLocation(locID)
In a Nightswim story the player will go from location to location. When switching locations it will check if a new background image needs to be displayed, whether a new audiotrack needs to be loaded and played, and whether the new location has custom CSS that needs to be applied to it.

Every location can have a list of scenes and/or cutscenes attached to it. When a player enters a new location the prioritization is as follows:
1. When a cutscene from the cutscenes-array is set to `true`, it will play.
2. When a scene from the scenes-array is set to `true`, it will run.
3. If neither is the case then the location's contents are shown. If either is the case, then this will happen after the cutscene or scene has ended. What happens is that first the old contents are faded out (by a call to `fadeOut(fadeTime)`, are then replaced (by calling `replaceById(fadeTime)`) and faded back in with a call to `fadeIn(fadeTime)`. These three functions can be found in display.js.

All code for cutscenes can be found in cutscene.js, and for scenes in scene.js.

### checkConditions(condObject)
This function handles all conditions (well doh ;-).

### change(changeObject)
This function handles all consequences.

## src/parse.js
Any story content will run through `parse(txt)`. Location content will additionally run through `parseLocation(txt)`.

`parse(txt)` detects location and interaction macro's. Location macro's look like this:
`[[button text->locationID]]` and will always be turned into buttons. A request to add a button will be added to either the regular buttonQueue (when the player is not in the interaction menu) or to the menuButtonQueue (when the interaction menu is open). `createButtons()` (from menu.js) will then create the actual buttons and attach event handlers later on.

Interaction macro's can look like this `{{button text->Obj-or-NpcID}}` and are then converted to buttons. Or they can be formatted like this `{{!Obj-or-NpcID}}`. In that case we have a *direct link*, which will be converted to an inline `<a href="#">` link which will call `directAction()` when clicked.

`parseLocation(txt)` detects macro's inside the sectionHTML-parameter in location objects.
If `((text))` is found then the conditions for that section will only apply to that text.
If `({text})` is found then this text will be turned into a link which will run the section's consequences when clicked.

## src/menu.js
Menu.js holds, not unsurprisingly, all code related to the interaction menu. Additionally it contains the code for creating and displaying buttons (even the ones outside of the interaction menu). Most important function here is then, of course, `createButtons()`. This function takes all queued buttons and links from the buttonQueues and turns them either in `<button>`'s or `<a href="#">`'s. Eventhandlers are then attached, based on the `type` of each button.

## Other
Most other modules are quite obvious in what they contain and do, so I hope the comments will be sufficient for those. Contact me if you happen to have any questions.