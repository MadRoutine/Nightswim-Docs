# Let's dive in
This tutorial is made up of 10 parts, and it assumes no knowlegde of programming.
1. [Installation](#chap1)
2. [Core concepts](#chap2)
3. [Adding Locations](#chap3)
4. [Adding Objects](#chap4)
5. [Adding Characters](#chap5)
6. [Adding Scenes](#chap6)
7. [Adding Cutscenes](#chap7)
8. [Changing Story Settings](#chap8)
9. [Publishing Your Story](#chap9)
10. [More info](#chap10)

## What you need to know
You don't need any programming skills or deep knowledge about HTML and CSS, but a few basics are required. I wrote a [super quick guide](https://github.com/MadRoutine/Nightswim-Docs/blob/master/Super%20Quick%20Technical%20Guide.md) that teaches you all you need to know about HTML, CSS and JSON in just a few minutes.

<a id="chap1"></a>
## 1. Installation

First of all you need to download the [story template](https://github.com/MadRoutine/Nightswim-Story-Template). Put it somewhere on your hard drive and rename it with your project's title.

Next you need a text editor (for editing the story's data files) and an app to preview your story. The [Nightswim Editor](https://github.com/MadRoutine/Nightswim-Editor) is designed for both these purposes. Unfortunately, there are currently no installers available for various reasons (mostly because it's quite expensive to get certificates for creating signed distributables). If you feel comfortable compiling from source then [build instructions can be found here](https://github.com/MadRoutine/Nightswim-Editor/blob/master/README.md). If not, then alternatively you can do the following:

For editing: download and install any code editor of choice (for example [Atom](https://atom.io/) or [VS Code](https://code.visualstudio.com/)). The template/tools folder contains a template generator that will generate prebuild blocks of game-data and copies them to your clipboard, so you can paste them in your code editor.

For previewing: download and install [Firefox](https://www.mozilla.org/en-US/firefox/new/), as it's the only browser that I know of that allows local AJAX requests (in other words: it's the only browser that will allow you to preview your story offline). You can also setup a local webserver instead.

This guide assumes the use of the Nightswim Editor, but you can also follow along when using alternative apps.

Let's have a look at the story template. It should look like this:
```
- dist/         (contains the Nightswim engine)
- lib/          (contains other libraries)
- story/        (contains your story)
    - audio/
    - scenes/
- tools/        (contains the JSON data generator)
- index.html    (open index.html in Firefox to preview your story)
- location.css  (CSS file where you can put custom classes for locations)
- menu.css      (CSS file for styling the interaction menu)
- style.css     (CSS file for the majority of your story's look)
```
The **story folder** is where
most of your work will be done. By default it contains four files: *init.json*,
*locations.json*, *npc_list.json* and *obj_list.json*. These files are gonna hold
your story's content and game logic. Additionally there will be scene files (to
be put in *story/scenes/*). Other content goes in their respective folders: *story/audio/*,
*story/images/* and *story/video/*.

<a id="chap2"></a>
## 2. Core concepts
Before we start building a story there are two important concepts that need to
be understood: *Conditions* and *Consequences*. You'll see these two throughout
the documentation, and you will use them frequently when defining your story's
game logic. They're pretty self-explanatory, but let's briefly talk about them:
### Conditions
When you define one or more conditions then all of these conditions have to be met
in order for something to happen in your story. Conditions can be applied to a
variety of things. For example: a condition for lifting a heavy rock might be
that the main character is not tired. [See the reference guide of different Condition-types.](https://github.com/MadRoutine/Nightswim-Docs/blob/master/Reference%20Guide%20-%20Conditions.md)
### Consequences
Consequences describe the changes that occur when the player performs an action
(for which the conditions are met). You can define multiple consequences per action.
[See the reference guide of different Consequence-types.](https://github.com/MadRoutine/Nightswim-Docs/blob/master/Reference%20Guide%20-%20Consequences.md)

<a id="chap3"></a>
## 3. Adding Locations
Nightswim works by defining locations and connecting these locations so that the
player can travel between them. Every location is made-up as a HTML-page, so
you can also think of locations as pages in your story.

So let's start by adding locations in
*story/locations.json*. Open the Nightswim Editor, click 'Open file', browse to your
story folder's location and open it. There's already one location defined in between
two brackets. It's important to understand that all your locations should go between these two
brackets. Nothing can come after it, because we're dealing with a JSON-file,
which can only contain a single object (or in this case: a single array; which is an object,
but don't think about that too much for now). Locations need to be separated by comma's.

Notice the first three parameters of your location:
- "locID": "start",
- "name": "",
- "accessMsg": "unlocked".

*locID* is the ID that you will use to reference this location later on in your
story. *name* can be left blank, as with the default settings it will not be
shown. If *accessMsg* is set to anything other than *unlocked*, the player
will not be able to enter this location, until *accessMsg* is set to
*unlocked* by a consequence.

Let's leave some others alone for now (they are described in the [full documentation](https://github.com/MadRoutine/Nightswim-Docs/blob/master/Reference%20Guide%20-%20Main%20Components.md))
and focus on *content*. *content* will be filled with *sections*. Every section
has a *sectionHTML* property, and this is where you'll write the stuff that
will be displayed when a player enters the location. You can add multiple
sections, but let's stick with one for now. Enter:

`"sectionHTML": "<p>Such a beautiful forest</p>[[Go north->forestNorth]]"`

What on earth means [[Go north->forestNorth]]? This is a *Location Macro* (we kindly borrowed/shamelessly copied these from Twine ;).
It will turn into a button that displays the text before the arrow, 'Go north'. Clicking the button
will change the location. The new location is specified by putting the locID on
the right side of the arrow. We can add our second location now and set its locID to
*forestNorth*. The forest will then link to forestNorth.

Important: location macro's are automatically detected and **removed** from sectionHTML, and added as
buttons underneath your content. If you want a location link within your
section, then you can hook up a *location-change consequence* to a section, and put the
linked text between `({ round and curly brackets })`. More information about conditions and consequences in relation to locations can be found in the [reference guide](https://github.com/MadRoutine/Nightswim-Docs/blob/master/Reference%20Guide%20-%20Main%20Components.md).

You can add another location by putting the text cursor after the closing
bracket of the entire block surrounding our location, that looks like this: `}`.
Add a comma to separate the locations and
click the *Location* button on the right of the editor (under "Main components"), or press the same button from the
template generator and paste it into your own code editor.

Put in "forestNorth" as locID, and fill in a short description in its
sectionHTML, followed by a location macro back to our first location: `[[Go
south->start]]`

Time to see what we did so far! Click the **Test Story** button on the top right to see what the story looks like so far (or press ALT/Option+S), or open the index.html in Firefox. You should be able to travel back and forth from the start location to forestNorth.

<a id="chap4"></a>
## 4. Adding Objects

Let's add an object that the player can interact with! Objects are defined in *story/obj_list.json*. Within the Nightswim Editor
you can simply click it in the left column (under "Main files") to open it. It will ask you if you want to save the file that's currently
open. Click "Save".

This file is empty (apart from two brackets). Put the cursor in between the brackets and add a standard object by
clicking "Obj" in the right column of the editor (under "Main components"). An object with all sorts of parameters will be
added now. If you like you can read what each of these parameters does in the [reference guide]
(https://github.com/MadRoutine/Nightswim-Docs/blob/master/Reference%20Guide%20-%20Main%20Components.md).

Let's keep it simple for now, though. `name` is the most important one, cause whatever you will fill in here will
be what you're going to refer to elsewhere in your story. We're going to add a stone that we can throw from one location
to the next. Replace `"objID"` with `"stone"` (keep the quotes), and `"descr"` with
`"It's a stone. It looks powerful. You feel a connection to this stone unlike anything you ever felt for other stones."`.
Then replace `"locID"` with `"start"`.
You might notice the sentence above is a bit long and therefore the editor gets a horizontal scrollbar. You can view longer
content on multiple lines within the editor by clicking the `Word Wrap` button in the right section of the black menu bar, or
by pressing ALT/Option+Z.

Save your file and go back to *locations.json*. Add ` A {{particular stone->stone}} grabs your attention.` in between
`What a beautiful forest.` and `[[Go North->forestNorth]]`. Here we have our second type of macro: an *Object Macro*.
This will be used to referenced the objects that we define in *obj_list.json*. The first part ("particular stone") will
become the text that will be displayed, and after the `->` arrow comes the name of the object that you want to refer to,
similar to how Location Macro's work.

Test your story. You will see that "particular stone" has been turned into a link. When you click it, a pop-up, called the
*Interaction Menu*, will display with the description we filled in, and two buttons: `ButtonTxt` and `Close`.

Save your file and go back to *obj_list.json*. Notice the parameter called `interactions`. This is an array that contains
all possible things the player can *do* with this object. Buttons for each interaction will be displayed in the aforementioned
Interaction Menu. That's why we saw a button with `ButtonTxt`. Change `"buttonTxt"` with `"throw stone"`. After an interaction
has been performed a feedback message will be shown. For the feedback parameter let's Fill in `"You threw the stone to the north"`.

Nothing will actually happen when a player clicks the "Throw stone" button, unless we specify the Consequence.
Put the cursor in between the brackets that follow `"consequences": `. In the right column of the editor you see a large list
of Consequences to choose from. Click `changeObjLoc`. We'd like to change the `location` parameter of the stone object to
`forestNorth`, so replace `"objID"` with `"stone"` and `"locationID"` with "`forestNorth"`. You might wonder why you need
to enter "stone" when we're already in the stone-object... This is because any action can trigger a location change for an
object, not just the stone itself.

If we now test the story and click the "Throw stone" button, the location parameter for the stone will change, yet you will not
see any difference! That's because the location itself doesn't check whether the objects in it are indeed in that location.
You need to add Conditions in order to display or not display certain bits of HTML. But since we changed the location parameter,
we can now add Conditions based on this parameter.

Conditions for locations are applied either to an entire section, or to a part of the section that is contained within a
*Condition Macro*. They look like this: `((Conditions only apply to everything here))`.
If we don't define a Condition Macro, then the conditions apply to the entire section. So let's add a condition only to
` A {{particular stone->stone}} grabs your attention.` by putting double round brackets around it:
`(( A {{particular stone->stone}} grabs your attention.))`
Put the cursor in between the square brackets after `"conditions": ` and click `location` from the list in the right column
of the editor, under "Conditions". This adds a location condition. Fill in the following values:

```json
{
    "type": "location",
    "obj": "stone",
    "value": "start",
    "failMsg": ""
}
```

Almost there! Let's add a similar section to our forestNorth location. Simply add
`(( A {{particular stone->stone}} grabs your attention.))` to its sectionHTML, and add a location condition
with the following values:

```json
{
    "type": "location",
    "obj": "stone",
    "value": "forestNorth",
    "failMsg": ""
}
```
Test your story. You can now throw the stone north! And when you change location, you will actually
find it there. Strangely though, you can repeatedly throw it north, even when
it's north already. What to do about that? Simple. We need to add a condition to the throw action.
In order to throw the stone north, the stone must be south, and vice versa.

Open *obj_list.json*, put your cursor in between the brackets after `"conditions": ` and click the
`location` condition in the right column under "Conditions", just like we did before. Again, fill in
`"stone"` as value for the `"obj"` parameter, and `"start"` as value for the `"value"` parameter.

Let's also add an interaction to throw the stone back south. Put the cursor at the end of the current
interaction (after the curly closing bracket), add a comma, an click the button in the right column:
Main components > Interaction. Replace `"buttonTxt"` with `"throw it back"`. Add a similar location condition,
but this time with `"forestNorth"` as value. Also add a similar changeObjLoc consequence, this time
with `"start"` as value.

Now test your story, and throw that stone back and forth.

<a id="chap5"></a>
## 5. Adding Characters
<a id="chap6"></a>
## 6. Adding Scenes
<a id="chap7"></a>
## 7. Adding Cutscenes
<a id="chap8"></a>
## 8. Changing Story Settings
<a id="chap9"></a>
## 9. Publishing Your Story
<a id="chap10"></a>
## 10. More info
- Flow of events when player enters a location
- Some other tips
- Links to documentation and references
