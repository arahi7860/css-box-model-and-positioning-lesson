
# CSS Box Model and Positioning

### Objectives
*After this lesson, students will be able to:*

- Describe the difference between block, inline, and inline-block elements
- Adjust element spacing using padding and margin
- Create floating elements to position content removed from the standard document flow
- Explain the difference between and use cases of static, relative, fixed, & absolute positioning
- Create a page with multicolumn layout

### Preparation
*Before this lesson, students should already be able to:*

- Write basic CSS
- Write basic HTML
- Use the chrome console

> Note: Solution code for this lesson is built out as the lesson progresses.

## An Intro to The Box Model


All HTML elements can be considered boxes. Even if you see a circle, it's living within a box.

The CSS box model describes this principal - a box wraps around all HTML elements, and it consists of: margins, borders, padding, and the actual content.  This model allows us to place a border around elements and space elements in relation to other elements.

With CSS properties and values, it is possible to apply specific styles to each of these elements, and change the way they behave and/or display on the page.

## Box Model Demo - Codealong

Let's write some HTML we can come back to and use to visualize what we're talking about.

- Create an new directory called `box-model-work`
- Create html page called `index.html` with an externally linked css stylesheet called `main.css`
- Inside your html page create a "container" div holding four divs within.
- Inside our CSS page, make the container a 500px gray square containing 100px squares within that are red, blue, green, and black.

Looking at the html:

```html
<!-- head section -->
<link rel="stylesheet" type="text/css" href="main.css">
```

```html
<!-- body section -->
<div id="squares-container">
    <div class="square1 square"></div>
    <div class="square2 square"></div>
    <div class="square3 square"></div>
    <div class="square4 square"></div>
</div>
```

And the CSS:

```css
#squares-container{
    width: 500px;
    background-color: gray;
}
.square1 {
    background-color: red;
}
.square2 {
    background-color: blue;

}
.square3 {
    background-color: green;
}
.square4 {
    background-color: black;
}

.square{
    height: 100px;
    width: 100px;
}
```

Dynamite!  Now, navigate to your dev tools and under the elements tab, hover over each of the divs.  What do you notice? A "box" is being highlighted in your browser!

How about if we drop this code into our CSS file:


```css
* {
    border: 1px solid red !important;
}
```

Notice the body, the container, and each of the divs are surrounded by a red border.  Peak at the styles tab on the right and scroll all the way to the bottom.  You'll notice boxes within boxes - madness!

## The Box Model and its components

The image below illustrates the box model and what you should have seen in your dev tools:

![box-model](https://mdn.mozillademos.org/files/13649/box-model-alt-small.png)

_From [www.theslate.org](http://www.theslate.org)_

But what do these different layers mean, and how are they relating to one another?


* **Margin** - clears an area around the border; the margin does not have a background color, it is completely transparent

* **Border** - a border that goes around the padding and content; the border is affected by the background color of the box

* **Padding** - clears an area around the content; the space between the content and the border; the padding is affected by the background color of the box

* **Content** - The content of the box, where text and images appear

#### Layers of the Box Model

Let's get go into some more detail and practice with each of these elements of The Box Model.


#### Margin

The margin is the space around the element. The larger the margin, the more space between our element and the elements around it. We can adjust the margin to move our HTML elements closer to or farther from each other.

Let's start with our margins. Adjusting our margins not only moves our element relative to other elements on the page but also relative to the "walls" of the HTML document.

For instance, if we take an HTML element with a specific width (such as our `<div>` in the editor) and set its margin to `auto` - this tells the document to automatically put equal left and right margins on our element, centering it on the page.

If you want to specify a particular margin, to a particular side, you can do it like this:

```css
div {
  margin-top: /*some value*/
  margin-right: /*some value*/
  margin-bottom: /*some value*/
  margin-left: /*some-value*/
}

```
> Note: Demonstrate altering each of these values in the dev tools for the div selector.

You can also set an element's margins all at once: you just start from the top margin and go around clockwise (going from top to right to bottom to left). For instance,

```css
div {
  margin: 1px 2px 3px 4px;
}
```

You can do top-bottom and side side - let's add this to our css for now:

```css
div {
  margin: 0 auto;
}
```

#### Border

We've talked briefly about borders - the border is the edge of the element. It's what we've been making visible every time we set the border property.

Borders can be set in two ways, just like your margins and just like we've talked about previously.

Lets add some thick borders to our `<div>`'s by removing the `!important` from the `*` selector and adding:

```css
div {
  margin: 0 auto;
  border: 5px solid black;
}
```

#### Padding and Content

The padding is the spacing between the content and the border. We can adjust this value with CSS to move the border closer to or farther from the content.

Padding can be set in two ways, just like your margins.

Lets add some padding to our `<div>`'s from our dev tools.  Notice, the space inside the "boxes" gets larger.  

```css
div {
  margin: 0 auto;
  border: 5px solid black;
  padding: 2px;
}
```

Update your CSS file to include this.

Padding becomes more apparent when we have "stuff" inside the box. If we're talking about a `<p>` element, the "stuff" is the text of the paragraph - the __content__. Let's add some text:

```html
<div id="squares-container">
    <p>hi there!</p>
    <div class="square1 square"></div>
    <div class="square2 square"></div>
    <div class="square3 square"></div>
    <div class="square4 square"></div>
</div>
```

_Note the way we're assigning two classes to each element; why? What does this achieve?_

Open the browser, and now, give that `p` tag some padding in the dev tools:

```css

p {
  padding: 20px;
}
```

Amazing!  Add those styles to your CSS file.


## Taking Up Space using Display

Cool, right? Each HTML element gets its own box to live in.

As you saw, the outermost box of each element went all the way across the page. This is why, until now, your HTML elements have been sitting on top of one another: by default, they take up the full width of the page.

We can change all this with the first positioning property we'll learn, the `display` property and the four values we can use: inline, block, inline-block, and none.

* An **inline** element:
    -  Has no line break before or after it. This makes the element sit on the same line as another element, but without formatting it like a block. It only takes up as much width as it needs (not the whole line).
    - Does not allow allow width, height, and margin top/bottom to be set;  in other word, it doesn't have the "boxy" quality of block element.

* A **block** element:
    -  Won't let anything sit next to it on the page and takes up the full width.
    - Is "boxy," and allows for setting width, height, and margin top/bottom.
 

* An **inline-block** element:
    - Is placed as an inline element (on the same line as adjacent content).
    - Is "boxy" in that it allows for custom width, height, and margin top/bottom.

* If you assign **none** as the value of the display, this will make the element and its content disappear from the page entirely!

To illustrate this, if we had this HTML:


```html
<div>
    <div class="inline content">inline</div>
    <div class="inline content">inline</div>
    <div class="inline content">inline</div>
</div>

<div>
    <div class="block content">block</div>
    <div class="block content">block</div>
    <div class="block content">block</div>
</div>

<div>
    <div class="inline-block content">inline-block</div>
    <div class="inline-block content">inline-block</div>
    <div class="inline-block content">inline-block</div>
</div>
```

With this CSS:

```css
.inline {
    display: inline;
}

.block {
    display: block;

}

.inline-block {
    display: inline-block;
}

.content{
    margin-top: 50px;
    width: 100px;
    height: 100px;
    border: 2px dotted red;
}

```


We would end up with something like this:

![display](/images/display.png)

> Note: Explain the styling in this image.

Try adding text before and after the elements themselves, and see how the different display elements respond.

## Positioning

Another CSS property, "position", can take `relative` or `absolute` values, among others.

A page element with "relative positioning" gives you the control to "absolutely position" children elements inside of it. This might not be obvious to everyone - that's probably because this isn't intuitive, at all. Let's look at an example.


![css position relative](https://i.imgur.com/LRd7lBy.png)

The relative positioning on the parent is what matters here. This what would happen if we forgot that:

![](https://i.imgur.com/0vGcPFL.png)

In this small example, it doesn't seem to matter much, but it really is a significant change.

⇒ The "absolutely positioned" elements are positioning themselves in relation to the body element, instead of their direct parent. So if the browser window grows, that element in the bottom left is going to stick with the browser window, not hang back inside, like it was the case in the previous example.

#### Relative Positioning

Declaring `position:relative` allows you to position the element top, bottom, left, or right relative to where it would normally occur.  Let's add some CSS and see what happens:

```css
.square1 {
    background-color: red;
    height: 100px;
    width: 100px;
    position:relative;
    top: 0;
    left: 40px;
}
```



#### Static Positioning

HTML elements are positioned static by default. A "static positioned" element is always positioned according to the normal flow of the page and are not affected by the top, bottom, left, and right properties.

Again, the default positioning for all elements is static. This means that no positioning has been applied and the elements occurs where they normally would in the document.

If we revisit our squares from earlier in class:

```css
#squares-container{
    background-color: gray;
    position: static;
    width: 500px;
}
```

You rarely explicitly declare `position:static` like this because it is the default.

#### Fixed Positioning

An element with fixed position is positioned relative to the browser window.  It will not move even if the window is scrolled, so a fixed positioned element will stay right where it is creating an effect a bit like the old school "frames" days.

Try it out:

```css
.square2 {
    position: fixed;
    width: 100%;
    height: 100px;
    background-color: blue;
    top: 0;
    left: 0;
}
```


#### Absolute Positioning

Specifying `position:absolute` _removes the element from the document_ and places it exactly where you tell it to be.

```css
.square1 {
    background-color: red;
    position:absolute;
    top: 0;
    right: 0;
}
```



##### Relative Positioning

Declaring `position:relative` allows you to position the element top, bottom, left, or right relative to where it would normally occur.

```css
.square1 {
    background-color: red;
    position:relative;
    top: 0;
    left: 40px;
}
```


## Conclusion

- Compare the elements of The Box Model - margin, border, padding, content.
- Compare inline-block, block, and inline.

## References and Further Reading
- [MDN Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Box_model)
