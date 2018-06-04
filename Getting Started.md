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
You don't need any programming skills or deep knowledge about HTML and CSS, but a few basics are required. I wrote a [super quick guide](link) that teaches you all you need to know about HTML, CSS and JSON in just a few minutes.

## 1. Installation {#chap1}

First of all you need to download the [story template](https://github.com/walterjohan/Nightswim-Story-Template). Put it somewhere on your hard drive and rename it with your project's title.

Next you need a text editor (for editing the story's data files) and an app to preview your story. The [Nightswim Editor](https://github.com/walterjohan/Nightswim-Editor) is designed for both these purposes. Unfortunately, there are currently no installers available for various reasons (mostly because it's quite expensive to get certificates for creating signed distributables). If you feel comfortable compiling from source then [build instructions can be found here](link). If not, then alternatively you can do the following:

For editing: download and install any code editor of choice (for example [Atom](https://atom.io/) or [VS Code](https://code.visualstudio.com/)). The template/tools folder contains a template generator that will generate prebuild blocks of game-data and copies them to your clipboard, so you can paste them in your code editor.

For previewing: download and install [Firefox](https://www.mozilla.org/en-US/firefox/new/), as it's the only browser that I know of that allows local AJAX requests (in other words: it's the only browser that will allow you to preview your story offline). You can also setup a local webserver instead.

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

## 2. Core concepts {#chap2}
Before we start building a story there are two important concepts that need to
be understood: *Conditions* and *Consequences*. You'll see these two throughout
the documentation, and you will use them frequently when defining your story's
game logic. They're pretty self-explanatory, but let's briefly talk about them:
### Conditions
When you define one or more conditions then all of these conditions have to be met
in order for something to happen in your story. Conditions can be applied to a
variety of things. For example: a condition for lifting a heavy rock might be
that the main character is not tired. [See the reference guide of different Condition-types.](link)
### Consequences
Consequences describe the changes that occur when conditions are met and an
action is performed. You can define multiple consequences per action.
[See the reference guide of different Consequence-types.](link)

## 3. Adding Locations {#chap3}
The easiest way to start your story is by adding locations in
*story/locations.json*. Open the Nightswim Editor, click 'Open file', browse to your
story folder's location and open it. At the start there's only two brackets.
It's important to understand that all your content should go between these two
brackets. Nothing can come after it.

Put the cursor in between the brackets and
click the *Location* button on the left (or press the same button from the
template generator and paste it into your own code editor). It will look like
this:
[screenshot]
Now simply fill in the information about the first location in between the blue
quotes:
- "locID": "forest",
- "name": "",
- "accessMsg": "unlocked".

*locID* is the ID that you will use to reference this location later on in your
story. *name* can be left blank, as with the default settings it will not be
shown. If *accessMsg* is set to anything other than *unlocked*, then the player
will initially not be able to enter this location, until *accessMsg* is set to
*unlocked* by a consequence.

Let's leave some others alone for now (they are described in the [full documentation](link))
and focus on *content*. *content* will be filled with *sections*. Every section
has a *sectionHTML* property, and this is where you'll write the stuff that
will be displayed when a player enters the location. You can add multiple
sections, but let's stick with one for now. Enter:

`<p>Such a beautiful forest</p>`

`[[Go north->forestNorth]]`

What on earth means [[Go north->forestNorth]]? This is a *Location Macro*. It will
turn into a button that displays the text before the arrow, 'Go north'. Clicking the button
will change the location. The new location is specified by putting the locID on
the right side of the arrow. We can add our second location now and set its locID to
*forestNorth*. The forest will then link to forestNorth.

Important: location macro's are automatically detected and **removed** from sectionHTML, and added as
buttons underneath your content. If you want a location link within your
section, then you can hook up a *location-change consequence* to a section, and put the
linked text between `({ round and curly brackets })`. More information about conditions and consequences in relation to locations can be found in the [reference guide](link).

You can add another location by putting the text cursor after the closing
bracket of the entire block surrounding our location, that looks like this: `}`.
Add a comma to separate the locations, then click the Location button again.

Put in "forestNorth" as locID, and fill in a short description in its
sectionHTML, followed by a location macro back to our first location: `[[Go
south->forest]]`

Time to see what we did so far! Click the **Test Story** button on the top right to see what the story looks like so far, or open the index.html in Firefox. You should be able to travel back and forth from forestNorth to forestSouth.

## 4. Adding Objects {#chap4}
## 5. Adding Characters {#chap5}
## 6. Adding Scenes {#chap6}
## 7. Adding Cutscenes {#chap7}
## 8. Changing Story Settings {#chap8}
## 9. Publishing Your Story {#chap9}
## 10. More info {#chap10}
- Flow of events when player enters a location
- Some other tips
- Links to documentation and references