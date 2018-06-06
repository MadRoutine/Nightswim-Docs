# Super Quick Technical Guide
This short guide briefly explains the following subjects:
- [JSON](#json)
- [HTML](#html)
- [CSS](#css)

<a id="json"></a>
## JSON
Game data is stored in JSON-files. You don't really need to know what that
means, but you need to understand a few formatting basics for JSON.

A .json file can store either of two types of Javascript data: an array or an object. An array is like a list containing data. It looks like this:

```json
[
    data,
    data,
    data
]
```

Notice the square brackets that enclose it, and notice how there's a comma whenever another item follows.

An object is similar, but there are keys (called *properties*) which are used to describe which data is stored. It looks like this:

```json
{
    "property1": data,
    "property2": data,
    "property3": data
}
```

Notice the curly brackets, and how the properties are defined between double quotes. A simple example of an object would look like this:

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "age": 32
}
```

The data can be of many different types: a number (*integer*), text (*string*),
true or false (*boolean*), or they can contain yet another array or object! This
way you can nest objects into objects into objects, etc. Note that when it comes
to data, only text and property-names will be put in double quotes.

Important to remember is that **text needs to be put on one line**. You cannot
press Enter and spread your text over multiple lines. Just toggle the *Word
Wrap* function in the editor when your lines get too long.

One last super important thing which I briefly mentioned at the top: **every JSON-file can only hold ONE array or object on the top level**. Inside this array or object you can nest as many other objects or arrays as you like, but on the top level there can be only one.

Let's look at an example of what it looks like to have an object within an array:
```json
[
    {
        "locID": "location ID",
        "accessMsg": "You can't go in here!"
    },
    {
        "locID": "ID of second location",
        "accessMsg": "unlocked"
    }
]
```
As you can see: the JSON-file contains one array. This array contains two objects, separated by a comma. Each object holds two properties, each with a string as data-type.

Okay, one more thing: since double quotes are used to mark the start and end of a string or property, you can't use them inside your string, unless you *escape* them. Escaping means you explicitly tell the software that a specific occurance of a character should be ignored. You escape a character by using a backward slash: `\`. So if you need to use double quotes within your string, it would look like this:

`"<p id=\"thisId\">"`

The double quotes that follow the backslash will now be ignored. Of course, this also means that if you happen to need to use a backslash in your text, you will also need to escape your backslash with... exactly: another backslash.

To learn more about JSON check out [W3Schools.com](https://www.w3schools.com/js/js_json_intro.asp)

<a id="html"></a>
## HTML
HTML is a language for formatting and displaying content. You don't apply formatting in a HTML document directly like you would in Word. Instead you mark certain portions of your content by putting so-called *tags* around them. Tags look like this:

`This sentence is displayed normally. <em>This sentence is displayed with emphasis.</em>`

As you can see: the closing-tag starts with a forward slash, to indicate that the emphasis should end there. On a screen it will look something like this:

This sentence is displayed normally. **This sentence is displayed with emphasis.**

Let's add another important tag: `<p>`. `<p>` is used to define a paragraph.

`<p>Start of paragraph. <em>Emphasis.</em> End of paragraph.</p>`

As you can see: tags can be *nested* inside one another. Tags can have attributes that provide extra information about them. You can use an *id* attribute for giving your tag a unique name, so it can be referenced somewhere else, or you can give it a *class* attribute, to give it certain styling (see CSS). An example:

`<p id="first_paragraph" class="introduction">First paragraph, will contain introduction text</p>`

An id is unique and can only be used for one tag, while you can give multiple tags the same class.

To learn more about HTML and HTML tags: [see W3Schools.com](https://www.w3schools.com/html/default.asp).

<a id="css"></a>
## CSS
Where HTML is used to divide your content into sections by marking them with tags, the way things will actually look on screen is defined in CSS. CSS is usually found in seperate .css files. In your Story template you will see three CSS files: *location.css*, *menu.css* and *style.css*. CSS looks like this:

```
element {
    color: black;
    background-color: white;
    position: relative;
    top: 10em;
    left: 10em;
}
```
The element can be a tag, like:
`p { color: purple; }`
will make all text inside every `<p>`-tag purple.

Or you can style everything with a certain id-attribute by using a hashtag (`#`), or a certain class with a dot:

`#first_paragraph { color: blue; }` will make the text color of whichever tag has the id 'first_paragraph' blue.

`.introduction { font-size: 0.8em; }` will make the font-size smaller for every tag that has the introduction-class.

You can also be more specific:

`p#first_paragraph { color: blue }` will only style a tag with id="first_paragraph" when it's a `<p>`-tag.

Same goes for classes:
`p.introduction { font-size: 0.8em }` will style every `<p>`-tag with the introduction class.

You can also choose to only style nested elements by using a space and then adding another element:

`p .introduction { font-size: 0.8em }` will style every tag inside the `<p>`-tag that has the introduction class.

To learn more about CSS: [see W3Schools.com](https://www.w3schools.com/css/default.asp).