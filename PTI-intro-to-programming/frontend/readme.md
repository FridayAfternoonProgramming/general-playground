# Frontend development for Non-Engineers

In this course,
we are going to learn the basics of frontend development:
HTML, CSS, and JavaScript.
No previous programming knowledge is needed.

Please take time to understand what you are doing
and ask a lot of questions!


## Requirements

- a laptop with internet access


### Setting up the Go fileserver

Create a file __server.go__ with the content:

```go
package main

import (
	"log"
	"net/http"
)

func main() {
	fs := http.FileServer(http.Dir("."))
	http.Handle("/", fs)
	log.Println("Listening...")
	http.ListenAndServe(":8080", nil)
}
```

run the server:

```
go run server.go
```

Let's determine the address of the cloud server, so that we can look at the API.
Run this command in the terminal:

```
curl http://169.254.169.254/latest/meta-data/public-hostname/
```

It prints something that looks like:

```
ec2-52-53-223-49.us-west-1.compute.amazonaws.com
```

That's a website address under which your server is running.
Try it out by copy-and-pasting it into the URL field in a new browser tab.
**Append `:8080` to the end, without spaces.**
The address should look something like this (just with different numbers):

```
http://ec2-52-53-223-49.us-west-1.compute.amazonaws.com:8080
```


## Overview of frontend technologies

The web is based on three technologies that work together
to form the rich experiences we have on the web today:
- __HTML__ defines the _textual content_ of websites and its structure
- __CSS__ defines the _layout_ of that content,
  i.e. how it is displayed to the user
- __JavaScript__ defines the _behavior_ of the content,
  i.e. what it does when you interact with it.

This course gives a quick introduction into all three.


## HTML

HTML is a __semi-structured document format__.
_Document format_ means that HTML contains human-readable text,
similar to MS Word documents.
Plain text without any formatting is valid HTML, web browsers can display it.

HTML is not really a technology to build applications.
One can build web applications like Slack inside an HTML document,
but they are basically just scripts displaying and populating
parts of a complex text document in real-time.

_Semi-structured_ means that HTML is not as fully structured
like for example data in a database.
In a database, the format and meaning of every element is exactly known.
HTML is plain text that can contain some amount of structure
for some parts of it, but not for others.
Let's explore this structure a bit.


### Hierarchical structure

HTML content is organized as a tree -
elements contain other elements.

<img src="tree.gif">

Let's create a simple HTML document,
look at a few of its elements,
and see what they do.


### Document Header and Body

Each HTML document consists of two parts:
- the __header__ contains only information about the document,
  like its title, who created it, what is it for, etc.
  We'll leave the header out for now to keep things simple,
  and add it later.
- the __body__ contains the actual text content of the document

Let's write some HTML!
Create a file __index.html__ with this content:

```html
<html>
  <body>
    Hello world!
  </body>
</html>
```

This is the smallest possible HTML document.
It just prints some unstructured text.
Some noteworthy features:
- tags are written as text in angle brackets
- `<html>` starts the _html_ tag
- `</html>` ends the _html_ tag
- `<body>` starts the _body_ tag
- `</body>` ends the _body_ tag
- the _html_ tag contains the _body_ tag
- the _body_ tag contains the text "Hello world!"
- the _body_ tag ends before the _html_ tag ends
  since it is strictly inside it
- indentation visualizes
  which element contains which other element


### Text Formatting

Change the content inside the `<body>` tag to look like this:

```html
CO<sub>2</sub> in the athmosphere leads to a <em>worldwide</em> greenhouse effect.
```

For reference, the entire document should look like this:

```html
<html>
  <body>
    CO<sub>2</sub> in the athmosphere leads to a <em>worldwide</em> greenhouse effect.
  </body>
</html>
```

The `<sub>` tag (short for _subscript_) around the `2`
causes it to be printed lower than normal text.
If you change `<sub>` and `</sub>` to `<sup>` and `</sup>`,
the `2` will be printed elevated.

The `<em>` tag around `worldwide` makes the text inside it look _emphasized_.
By default, the browser renders emphasized text italic.

To emphasize this text even stronger,
change `<em>` and `</em>` to `<strong>` and `</strong>`.
By default, the browser renders strongly emphasized text bold.


### Links

Time for the most ingenius piece of web technology that glues it all together -
hyperlinks!
Let's make the text `greenhouse effect` a link to the Wikipedia article about it:
change `greenhouse effect` to

```html
<a href="https://en.wikipedia.org/wiki/Greenhouse_effect">greenhouse effect</a>
```

For reference, the entire document should look like this:

```html
<html>
  <body>
    CO<sub>2</sub> in the athmosphere leads to a <em>worldwide</em> <a href="https://en.wikipedia.org/wiki/Greenhouse_effect"> greenhouse effect </a>.
  </body>
</html>
```

Check that the link works by refreshing the browser.

Links are created by an `<a>` HTML tag (which stands for _anchor_).
This tag contains an __attribute__ with the _name_ `href`
(wich means "hypertext reference")
and the _value_ `https://en.wikipedia.org/wiki/Greenhouse_effect`.
That's the address that the user goes to when clicking on the link.
The text between the opening `<a>` and closing `</a>` tag is the text
with which the link is displayed in the document.


## Newlines

The text inside the `body` element is getting a bit long and unwieldy.
Let's break it into several lines, to look like this:


```html
<body>
  CO<sub>2</sub> in the athmosphere
  leads to a <em>worldwide</em>
  <a href="https://en.wikipedia.org/wiki/Greenhouse_effect">
    greenhouse effect
  </a>.
</body>
```

As we can see, the output does not change.
HTML ignores newlines.
This comes in handy for programmers like us right now.
They can keep large amounts of HTML organized
in a way that is easy to read for them.

If you need to create a new line, use the `<br>` tag:

```html
<body>
  CO<sub>2</sub> in the athmosphere<br>
  leads to a <em>worldwide</em><br>
  <a href="https://en.wikipedia.org/wiki/Greenhouse_effect">
    greenhouse effect
  </a>.
</body>
```

### Tables

The Wikipedia page gives on overview of the various greenhouse gases.
Let's add a table with them to our document.
In HTML, tables work this way:
- a table contains many rows
- a row contains many cells
- there are two types of cells: _header cells_ (for captions) and _data cells_

To add a table, put this content on a new line after the `<a>` tag,
but before the `</body>` tag.

```html
<table>

  <!-- a row with the table captions -->
  <tr>
    <th>name</th>
    <th>contribution</th>
  </tr>

  <!-- the first data row -->
  <tr>
    <td>water vapor</td>
    <td>36-70%</td>
  </tr>

</table>
```

What is happening here?
- the `<table>` tag defines a table
- the `<tr>` tag ("table row") defines a row in this table
- the `<th>` tag ("table header") defines header cells inside the table,
  which the browser renders in bold by default
- the `<td>` tag ("table data") defines a data cell inside the table
- the `<!-- text -->` tag contains a comment for ourselves - it is not displayed

The preview window shows a table with two rows now.
Let's add the other greenhouse gases into the table.

```html
<!-- the second data row -->
<tr>
  <td>carbon dioxide</td>
  <td>9-26%</td>
</tr>

<!-- the third data row -->
<tr>
  <td>methane</td>
  <td>4-9%</td>
</tr>

<!-- the fourth data row -->
<tr>
  <td>ozone</td>
  <td>3-7%</td>
</tr>
```


### Headings

The content looks a bit mushed together.
Let's add headers to structure it a bit.
First, let's add a caption for the entire document.
Add this line right after the line that contains `<body>`:

```html
<h1>The Greenhouse Effect</h1>
```

`<h1>` means _heading level 1_.
A level 1 heading is the most important one in the document.
It describes the entire document and is rendered as very large text.

Next, let's add a caption for the section with the table
in a separate line above the `<table>` tag:

```html
<h2>Greenhouse gases on Earth</h2>
```

A level 2 heading describes sections of the document
and is rendered smaller than level 1 headings.


For reference, the end result should look like this:

```html
<html>
  <body>

    <h1>The Greenhouse Effect</h1>

    CO<sub>2</sub> in the athmosphere
    leads to a <em>worldwide</em>
    <a href="https://en.wikipedia.org/wiki/Greenhouse_effect">greenhouse effect</a>.

    <h2>Greenhouse gases on Earth</h2>

    <table>

      <!-- a row with the table captions -->
      <tr>
        <th>name</th>
        <th>contribution</th>
      </tr>

      <!-- the first data row -->
      <tr>
        <td>water vapor</td>
        <td>36-70%</td>
      </tr>

      <!-- the second data row -->
      <tr>
        <td>carbon dioxide</td>
        <td>9-26%</td>
      </tr>

      <!-- the third data row -->
      <tr>
        <td>methane</td>
        <td>4-9%</td>
      </tr>

      <!-- the fourth data row -->
      <tr>
        <td>ozone</td>
        <td>3-7%</td>
      </tr>

    </table>
  </body>
</html>
```


## CSS

We now have a small document with interesting content to read.
It doesn't look very modern, though.
Let's fix that by adding layout information.

### Loading CSS files

CSS is typically stored in a seperate file, for example `styles.css`. Create that file now in the root directory of your project. No need to add content yet. To load the CSS file, you must link to it from the HTML file which you created earlier:


```html
<html>
  <head>
    <link href="styles.css" rel="stylesheet">
  </head>
</html>
```

Perfect, now you're able to add css definitions to your HTML page.

### Font

First, let's fix that outdated font.
Google provides a number of modern fonts that we can use on websites.
You can see them at https://fonts.google.com.
Let's use the one called "Open Sans".

Using external fonts is done in two steps:
1. make the font known to our document
2. display parts of the document in this font

The first part is done in the document header.
This section of the document doesn't exist yet, so let's create it.
It comes after the `<html>` tag, before the `<body>` tag:

```html
<head>
  <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
  <link href="styles.css" rel="stylesheet">
</head>
```

For reference, this beginning of the HTML file looks like this now:

```html
<html>
  <head>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
    <link href="styles.css" rel="stylesheet">
  </head>
  <body>
    ...
```

Next we specify which parts of the document should use it.
We want to apply it to the entire document,
i.e. everything inside the `<body>` tag.
In the _CSS_ input field at the top right, enter:

```css
body {
  font-family: 'Open Sans', sans-serif;
}
```

This CSS element tells the browser that the entire body of the document
should use the `Open Sans` font that we just added to the page.
And if that font is not available,
the browser should use a built-in font called `sans-serif`.

CSS is a different programming language than HTML,
so it uses a different text format.
CSS does not contain tags in angle-brackets like HTML does.
Instead, it defines style attributes for HTML tags as key/value pairs.
In our case, we define style attributes for the HTML tag called `body`.
The first attribute we define has the name `font-family`
and the value `'Open Sans', sans-serif`.
We will add more attributes for the `body` tag in a minute.
The semicolon at the end of the line means that the `font-family` statement is over here,
and the next line talks about something else.
Now the web page is displayed with a nicer looking font.


### Colors

Next, let's change the background color of the document.
In CSS, the background color of elements on the page is done like this:

```css
background-color: yellow;
```

Yellow is a bit too intense for the page background, though.
Let's look at a list of colors available in HTML:
https://htmlcolorcodes.com/color-names
If you want to create your own color, you can also do that at
https://htmlcolorcodes.com/color-picker.
For now, we'll go with a font called `cornsilk`.
We also want to apply it to the entire body of the document,
so we write it as an additional attribute for the `body` tag:

```css
body {
  font-family: 'Open Sans', sans-serif;
  background-color: cornsilk;
}
```

It's also possible to define more complex background patterns, for example background images. To load a resource from a remote location - in this case pexels.com - wrap the URL with the `url()` function.

```css
body {
  background-image: url("https://static.pexels.com/photos/247041/pexels-photo-247041.jpeg");
  
  /* previous code */
  background-color: cornsilk;
  font-family: 'Open Sans', sans-serif;
}
```

By the way, you can use images from pexels for personal and commercial projects for free!

If you define both a background image and a background color, the background color will be used as fallback if the image can not be located:

```css
body {
  background-image: url("this url does not exist");

  /* previous code */
  background-color: cornsilk;
  font-family: 'Open Sans', sans-serif;
}
```

While we are at it,
let's also give the different heading types different colors:

```css
h1 {
  color: seagreen;
}

h2 {
  color: teal;
}
```

The table could use some love as well.
Let's use alternating colors for the table rows:

```css
tr:nth-child(even){
  background-color: blanchedalmond;
}
```

This means:
Give all the even table rows (i.e. the `<tr>` tags number 2, 4, 6, etc)
the background color `blanchedalmond`.


### Alignment

Next, let's make both heading types horizontally centered on the page.

```css
h1, h2 {
  text-align: center;
}
```

The second heading could use a bit more space before it,
right now this all looks a bit jammed.
Let's add an additional attribute called `margin-top` to the
style definition of `h2` elements:

```css
h2 {
  color: teal;        /* this line already exists */
  margin-top: 40px;   /* this line is added       */
}
```

Comments in CSS look like this: `/* text */`
You don't have to add the comments to the document,
they are just there for you to find the line to add.


### Spacing

The table cells are as wide as the text in them.
That's great, but it looks a bit cramped.
let's add some empty space (called _padding_ in CSS) around the text:

```css
th, td {
  padding-left: 30px;
  padding-right: 30px;
  padding-top: 7px;
  padding-bottom: 7px;
}
```

This adds 30 pixels of space to the top and bottom of table cells,
and 7 pixels to their left and right side.

To get rid of the gap between the two columns in the table:

```css
table {
  border-collapse: collapse;
}
```

This "collapses" the borders between table cells, i.e. removes them.

## Adding a Navigation

Let's combine all the knowledge so and add a navigation bar to our website with HTML and CSS. As the navigation bar is the first item on the webpage, the navigation element will be the first element in the body. To define a navigation, we will use the `<nav>` tag.


```html
<html>
  <head>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
    <link href="styles.css" rel="stylesheet">
  </head>
  <body>
    <nav>
	...
    </nav>
```

Next, you probably want to add some links to you navigation:


```html
<nav>
  <a href="/">Home</a>
  <a href="https://en.wikipedia.org/wiki/Greenhouse_effect">Wikipedia Article</a>
</nav>
```

That's great, but not beautiful. We will change that now. First, the navigation should be visible even if we scroll the page. This is possible by using `position: fixed`:

```css
nav {
  position: fixed;
}
```

The navigation should also be visually separated. We can do that by defining a background color for the item. For flashy use, we will use a color that has opacity. Colors with opacity are defined with `rgba`:

```css
nav {
  position: fixed;
  background-color: rgba(102, 153, 0, .7);
}
```

This looks strange now. We have to give the element a bit of spacing (using `padding`) and also make it full width (using `width`):

```css
nav {
  position: fixed;
  background-color: rgba(102, 153, 0, .7);
  padding: 20px;
  width: 100%;
}
```

The positioning of the element is still off. This is caused by `position: fixed`. Let's change that using `top` and `left`:


```css
nav {
  position: fixed;
  background-color: rgba(102, 153, 0, .7);
  padding: 20px;
  width: 100%;
  
  top: 0;
  left: 0;
}
```

The last thing we want to do is give the first heading element a bit of spacing to the top. Here we will use `margin-top` which is the spacing around the element, whereas `padding` is the spacing within the element. Update the `h1` rule from earlier:

```css
h1 {
  color: seagreen;
  
  margin-top: 50px;
}
```
