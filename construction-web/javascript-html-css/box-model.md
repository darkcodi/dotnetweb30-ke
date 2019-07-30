# Box model

The “CSS box model“ is a set of rules that define how every web page on the Internet is rendered. CSS treats each element in your HTML document as a “box” with a bunch of different properties that determine where it appears on the page. So far, all of our web pages have just been a bunch of elements rendered one after another. The box model is our toolkit for customizing this default layout scheme.

![Diagram: CSS stylesheet broken down into two parts \(text formatting and the box model\)](https://internetingishard.com/html-and-css/css-box-model/css-html-and-the-box-model-9d82a2.png)

A big part of your job as a web developer will be to apply rules from the CSS box model to turn a design mockup into a web page. 



Back in _Basic Web Pages_, we briefly touched on [how CSS uses “boxes”](https://internetingishard.com/html-and-css/basic-web-pages/#emphasis-italic-elements) to define the layout of a web page. Each HTML element rendered on the screen is a box, and they come in two flavors: “block” boxes and “inline“ boxes.

![Diagram: comparison of block boxes with inline boxes](https://internetingishard.com/html-and-css/css-box-model/inline-vs-block-boxes-f3e662.png)

All the HTML elements that we’ve been working with have a default type of box. For instance, `<h1>` and `<p>` are block-level elements, while `<em>` and`<strong>` are inline elements. Let’s get a better look at our boxes by adding the following to `box-styles.css`:

```text
h1, p {
  background-color: #DDE0E3;    /* Light gray */
}

em, strong {
  background-color: #B2D6FF;    /* Light blue */
}
```

The `background-color` property only fills in the background of the selected box, so this will give us a clear view into the structure of the current sample page. Our headings and paragraphs should have gray backgrounds, while our emphasis and strong elements should be light blue.

![Web page highlighting block boxes in gray and inline boxes in blue](https://internetingishard.com/html-and-css/css-box-model/block-boxes-and-inline-boxes-7cfa0a.png)

This shows us a couple of very important behaviors associated with block and inline boxes:

* **Block boxes** always appear **below** the previous block element. This is the “natural” or “static” flow of an HTML document when it gets rendered by a web browser.
* The **width of block boxes** is set automatically based on the width of its parent container. In this case, our blocks are always the width of the browser window.
* The default **height of block boxes** is based on the content it contains. When you narrow the browser window, the `<h1>` gets split over two lines, and its height adjusts accordingly.
* **Inline boxes** don’t affect **vertical spacing**. They’re not for determining layout—they’re for styling stuff _inside_ of a block.
* The **width of inline boxes** is based on the content it contains, not the width of the parent element.

### changing box behavior

For example, if we wanted to make our `<em>` and `<strong>` elements blocks instead of inline elements, we could update our rule in `box-styles.css` like so:

```css
em, strong {
  background-color: #B2D6FF;
  display: block;
}
```

Now, these elements act like our headings and paragraphs: they start on their own line, and they fill the entire width of the browser. This comes in handy when you’re trying to turn `<a>` elements into buttons or format `<img/>` elements \(both of these are inline boxes by default\).

![Web page showing what happens when you turn inline boxes into block boxes with the CSS display property](https://internetingishard.com/html-and-css/css-box-model/turning-inline-into-block-boxes-772f4c.png)

However, it’s almost never a good idea to turn `<em>` and `<strong>` into block elements, so let’s turn them back into inline boxes by changing their `display` property to `inline`, like so:

```css
em, strong {
  background-color: #B2D6FF;
  display: inline;             /* This is the default for em and strong */
}
```

### content, padding, border, and margin

The “CSS box model” is a set of rules that determine the dimensions of every element in a web page. It gives each box \(both inline and block\) four properties:

* **Content** – The text, image, or other media content in the element.
* **Padding** – The space between the box’s content and its border.
* **Border** – The line between the box’s padding and margin.
* **Margin** – The space between the box and surrounding boxes.

Together, this is everything a browser needs to render an element’s box. The content is what you author in an HTML document, and it’s the only one that has any semantic value \(which is [why it’s in the HTML](https://internetingishard.com/html-and-css/basic-web-pages/#structure-versus-presentation)\). The rest of them are purely presentational, so they’re defined by CSS rules.

![Diagram: content, padding, border, and margins making up the CSS box model](https://internetingishard.com/html-and-css/css-box-model/css-box-model-73a525.png)

### padding

The `padding` property…you guessed it…defines the padding for the selected element:

```css
h1 {
  padding: 50px;
}
```

![Web page showing increase in &amp;lt;h1&amp;gt; padding \(background size increases\)](https://internetingishard.com/html-and-css/css-box-model/increasing-heading-padding-5a289d.png)

Sometimes you’ll only want to style one side of an element. For that, CSS provides the following properties:

```css
p {
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 10px;
  padding-right: 10px;
}
```

### shorthand formats

![Diagram: CSS padding property with vertical and horizontal values highlighted](https://internetingishard.com/html-and-css/css-box-model/padding-shortform-two-values-a7ed4c.png)

This means that our previous rule can be rewritten as:

```css
p {
  padding: 20px 10px;  /* Vertical  Horizontal */
}
```

Alternatively, if you provide _four_ values, you can set the padding for each side of an element individually. The values are interpreted clockwise, starting at the top:

![Diagram: CSS padding property with top, right, bottom, and left values highlighted](https://internetingishard.com/html-and-css/css-box-model/padding-shortform-four-values-93c021.png)

```css
p {
  padding: 20px 0 20px 10px;  /* Top  Right  Bottom  Left */
}
```

### borders

![Diagram: CSS border property showing size, style, and color syntax](https://internetingishard.com/html-and-css/css-box-model/css-border-syntax-d8ba17.png)

Try adding a border around our `<h1>` heading by updating the rule in `box-styles.css`:

```css
h1 {
  padding: 50px;
  border: 1px solid #5D6063;
}
```

This tells the browser to draw a thin gray line around our heading. Notice how the border bumps right up next to the padding with no space in between. And, if you shrink your browser enough for the heading to be split over two lines, both the padding and the border will still be there.

Drawing a border around our entire heading makes it look a little 1990s, so how about we limit it to the bottom of the heading? Like `padding`, there are `-top`, `-bottom`, `-left`, and `-right` variants for the `border` property:

```css
border-bottom: 1px solid #5D6063;
```

### margins

Margins define the space outside of an element’s border.

```css
p {
  padding: 20px 0 20px 10px;
  margin-bottom: 50px;          /* Add this */
}
```

Margins and padding can accomplish the same thing in a lot of situations, making it difficult to determine which one is the “right” choice. The most common reasons why you would pick one over the other are:

* The padding of a box has a background, while margins are always transparent.
* Padding is included in the click area of an element, while margins aren’t.
* Margins collapse vertically, while padding doesn’t \(we’ll discuss this more in the next section\).

### margins on inline elements

```css
strong {
  margin: 50px;
}
```

The horizontal margins display just like we’d expect, but this doesn’t alter the vertical space around our `<strong>` element one bit.

![Web page demonstrating lack of vertical margins on inline boxes](https://internetingishard.com/html-and-css/css-box-model/margins-on-inline-elements-4c569c.png)

If we change `margin` to `padding`, we’ll discover that this isn’t exactly the case for a box’s padding. It’ll display the blue background; however, it won’t affect the vertical layout of the surrounding boxes.

![Web page demonstrating vertical padding on inline boxes](https://internetingishard.com/html-and-css/css-box-model/paddings-on-inline-elements-fb52d0.png)

The rationale behind this goes back to the fact that inline boxes format runs of text inside of a block, and thus have limited impact on the overall layout of a page.

### vertical margin collapse

Another quirk of the CSS box model is the “vertical margin collapse”. When you have two boxes with vertical margins sitting right next to each other, they will collapse. Instead of adding the margins together like you might expect, only the biggest one is displayed.

For example, let’s add a top margin of 25 pixels to our `<p>` element:

```css
p {
  padding: 20px 0 20px 10px;

  margin-top: 25px;
  margin-bottom: 50px;
}
```

Each paragraph should have 50 pixels on the bottom, and 25 pixels on the top. That’s 75 pixels between our `<p>` elements, right? Wrong! There’s still only going to be `50px` between them because the smaller top margin collapses into the bigger bottom one.

![Diagram: comparison of an uncollapsed vertical margin with a collapsed vertical margin](https://internetingishard.com/html-and-css/css-box-model/vertical-margin-collapse-bba78e.png)

This behavior can be very useful when you’re working with a lot of different kinds of elements, and you want to define their layout as the _minimum_ space between other elements.

### generic boxes

 Both `<div>` and `<span>` are “container” elements that don’t have any affect on the semantic structure of an HTML document. They do, however, provide a hook for adding CSS styles to arbitrary sections of a web page. 

```markup
<div>Button</div>
```

And here are the associated styles that need to go into `box-styles.css`. Most of these should be familiar from the last chapter, although we did throw in a new [`border-radius` property](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius):

```css
div {
  color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
}
```

This will give us a big blue button that spans the entire width of the browser:

![Web page using &amp;lt;div&amp;gt; elements for buttons](https://internetingishard.com/html-and-css/css-box-model/generic-div-for-button-70dc27.png)

### content boxes and border boxes

![Diagram: content-box measurements adding padding and border to width of the element](https://internetingishard.com/html-and-css/css-box-model/box-sizing-content-box-09f48a.png)

SS lets you change how the width of a box is calculated via the `box-sizing` property. By default, it has a value of `content-box`, which leads to the behavior described above. Let’s see what happens when we change it to `border-box`:

```css
div {
  color: #FFF;
  background-color: #5995DA;
  font-weight: bold;
  padding: 20px;
  text-align: center;
  border: 2px solid #5D6063;
  border-radius: 5px;
  
  width: 200px;
  box-sizing: border-box;  /* Add this */
}
```

This forces the actual width of the box to be `200px`—including padding and borders. Of course, this means that the content width is now determined automatically:

![Diagram: border-box measurements including padding and border with the width of the element](https://internetingishard.com/html-and-css/css-box-model/box-sizing-border-box-ace2be.png)

### resetting styles

![One web page showing white border due to default margin/padding and another web page without the white border after a universal reset](https://internetingishard.com/html-and-css/css-box-model/resetting-box-sizing-and-margins-72ff64.png)

It’s usually a good idea to override default styles to a predictable value using the “universal” CSS selector \(`*`\). Try adding this to the top of our `box-styles.css` file:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

### summary

With a few key concepts from this chapter, you should feel much more equipped to convert a design mockup into a real-life web page:

* Everything is a box.
* Boxes can be inline or block-level.
* Boxes have content, padding, borders, and margins.
* They also have seemingly arbitrary rules about how they interact.
* Mastering the CSS box model means you can lay out most web pages.

