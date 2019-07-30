# HTML: Basic elements

HTML defines the content of every web page on the Internet. By “marking up” your raw content with HTML tags, you’re able to tell web browsers how you want different parts of your content to be displayed. Creating an HTML document with properly marked up content is the first step of developing a web page.

![Diagram: raw content turning into HTML markup turning into a web page](https://internetingishard.com/html-and-css/basic-web-pages/html-markup-0761f7.png)

 Add the following HTML markup to our `basics.html` file.

```markup
<!DOCTYPE html>
<html>
  <head>
    <!-- Metadata goes here -->
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```

 First, we need to tell browsers that this is an HTML5 web page with the`<!DOCTYPE html>` line. This is just a special string that browsers look for when they try to display our web page, and it always needs to look exactly like it does above.

### `html`

Then, our entire web page needs to be wrapped in `<html>` tags. The actual `<html>` text is called an “opening tag”, while `</html>` is called a “closing tag”. Everything inside of these tags are considered part of the `<html>`“element”, which is this ethereal thing that gets created when a web browser parses your HTML tags.

![Diagram: an HTML element composed of an opening tag and a closing tag](https://internetingishard.com/html-and-css/basic-web-pages/html-tags-elements-72813b.png)

Inside of the `<html>` element, we have two more elements called `<head>` and `<body>`. A web page’s head contains all of its metadata, like the page title, any CSS stylesheets, and other things that are required to render the page but you don’t necessarily want the user to see. The bulk of our HTML markup will live in the `<body>` element, which represents the visible content of the page. Note that opening up our page in a web browser won’t display anything, since it has an empty `<body>`.

![Diagram: web page split into &amp;lt;head&amp;gt; and&amp;lt;body&amp;gt; elements](https://internetingishard.com/html-and-css/basic-web-pages/html-head-body-7c2a73.png)

 Also notice the HTML comment syntax in the above snippet. Anything that starts with `<!--` and ends with `-->` will be completely ignored by the browser. This is useful for documenting your code and making notes to yourself.

### `title`

 One of the most important pieces of metadata is the title of your web page, defined by the aptly named `<title>` element. 

Try updating our `basic.html` file’s `<head>` to match the following:

```markup
<!DOCTYPE html>
<html>
  <head>
    <title>Interneting Is Easy!</title>
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```

When you reload the page in your browser, you should still see an empty page, but you’ll also see **Interneting Is Easy!** in the browser tab:

![Web page showing &amp;lt;title&amp;gt; element displayed in a browser tab](https://internetingishard.com/html-and-css/basic-web-pages/html-title-element-f4eb85.png)

### paragraph



The `<p>` element marks all the text inside it as a distinct paragraph. Try adding the following `<p>` element to the body of our web page:

```markup
<p>First, we need to learn some basic HTML.</p>
```

![](../../.gitbook/assets/image%20%28101%29.png)

### Headings

Headings are like titles, but they’re actually displayed on the page. HTML provides six levels of headings, and the corresponding elements are: `<h1>`, `<h2>`, `<h3>`, … , `<h6>`. The higher the number, the less prominent the heading.

The first heading on a page should typically be an `<h1>`, so let’s insert one above our existing `<p>` element. It’s very common for the first `<h1>` element to match the `<title>` of the document, as it does here:

```markup
<body>
  <h1>Interneting Is Easy!</h1>
  <p>First, we need to learn some basic HTML.</p>
</body>
```

![Web page showing a big &amp;lt;h1&amp;gt; element and a smaller&amp;lt;h2&amp;gt; element](https://internetingishard.com/html-and-css/basic-web-pages/html-heading-elements-f7fe6a.png)

Headings are the primary way you mark up different sections of your content. They define the outline of your web page as both humans and search engines see it, which makes selecting relevant headings essential for a high-quality web page.

### unordered list

Whenever you surround a piece of text with HTML tags, you’re adding new meaning to that text. Wrapping content in `<ul>` tags tells a browser that whatever is inside should be rendered as an “unordered list”. To denote individual items in that list, you wrap them in `<li>` tags, like so:

```markup
<h2>Lists</h2>

<p>This is how you make an unordered list:</p>

<ul>
  <li>Add a "ul" element (it stands for unordered list)</li>
  <li>Add each item in its own "li" element</li>
  <li>They don't need to be in any particular order</li>
</ul>
```

![Web page showing a &amp;lt;ul&amp;gt; with&amp;lt;li&amp;gt; elements inside of it](https://internetingishard.com/html-and-css/basic-web-pages/html-unordered-lists-f45526.png)

The HTML specification defines strict rules about what elements can go inside other elements. In this case, `<ul>` elements should only contain `<li>`elements, which means you should never ever write something like this:

```markup
<!-- (This is bad!) -->
<ul>
  <p>Add a "ul" element (it stands for unordered list)</p>
</ul>
```

Instead, you should wrap that paragraph with `<li>` tags:

```markup
<!-- (Do this instead) -->
<ul>
  <li><p>Add a "ul" element (it stands for unordered list)</p></li>
</ul>
```

### ordered list

If the sequence of list items does matter, you should use an “ordered list” instead. To create an ordered list, simply change the parent `<ul>` element to `<ol>`. Append the following content to the **Lists**section of `basics.html`:

```text
<p>This is what an ordered list looks like:</p>

<ol>
  <li>Notice the new "ol" element wrapping everything</li>
  <li>But, the list item elements are the same</li>
  <li>Also note how the numbers increment on their own</li>
  <li>You should be noticing things is this precise order, because this is
      an ordered list</li>
</ol>
```

When you reload the page in your browser, you’ll notice that the browser automatically incremented the count for each `<li>` element. 

![Web page showing a &amp;lt;ol&amp;gt; with&amp;lt;li&amp;gt; elements inside of it](https://internetingishard.com/html-and-css/basic-web-pages/html-ordered-lists-120411.png)

The difference between an unordered list and an ordered list might seem silly, but it really does have significance to web browsers, search engines, and, of course, human readers. It’s also easier than manually numbering each list item.

{% hint style="info" %}
 Step-by-step procedures like recipes, instructions, and even tables of contents are good candidates for ordered lists, while `<ul>` lists are better for representing item inventories, product features, pro/con comparisons, and navigational menus.
{% endhint %}

### emphasis \(italic\) elements

 The other major type of content is “inline elements” or “phrasing content”, which are treated a little bit differently. Block-level elements are always drawn on a new line, while inline elements can affect sections of text anywhere within a line.

![Diagram: comparison of block elements \(wrapping several inline elements\) with inline elements \(inside of a block element\)](https://internetingishard.com/html-and-css/basic-web-pages/inline-vs-block-elements-44860e.png)

For instance, `<p>` is a block-level element, while `<em>` is an inline element that affects a span of text _inside_ of a paragraph. It stands for “emphasis”, and it’s typically displayed as italicized text. Try adding a new section demonstrating emphasized text to our example web page:

```markup
<h2>Inline Elements</h2>

<p><em>Sometimes</em>, you need to draw attention to a particular word or
phrase.</p>
```

The part wrapped in `<em>` tags should render as italics, as shown below. 

![Web page highlighting the italic text created with an &amp;lt;em&amp;gt; element](https://internetingishard.com/html-and-css/basic-web-pages/html-emphasis-element-87be03.png)

### strong \(bold\) elements

If you want to be more emphatic than an `<em>` tag, you can use `<strong>`. It’s an inline element just like `<em>`, and looks like this:

```markup
<p>Other times you need to <strong>strong</strong>ly emphasize the importance
of a word or phrase.</p>
```

It should be rendered in bold text, like so:

![Web page highlighting the bold text created with a &amp;lt;strong&amp;gt; element](https://internetingishard.com/html-and-css/basic-web-pages/html-strong-element-d3135f.png)

To draw even more attention your a span of text, you can nest a `<strong>`element in an `<em>` element \(or vice versa\). This will give you text that is both strong and emphasized:

```markup
<p><em><strong>And sometimes you need to shout!</strong></em></p>
```

![](../../.gitbook/assets/image%20%28165%29.png)

### structure versus presentation

HTML markup should provide _semantic_information about your content—not _presentational_ information. In other words, HTML should define the structure of your document, leaving its appearance to CSS.

![Diagram: HTML as an abstract tree of nodes compared to CSS as various types of rendered text](https://internetingishard.com/html-and-css/basic-web-pages/structure-vs-presentation-05c228.png)

The pseudo-obsolete `<b>` and `<i>` elements are classic examples of this. They used to stand for “bold” and “italic”, respectively, but HTML5 attempted to create a clear separation between a document’s structure and its presentation. Thus, `<i>` was replaced with `<em>`, since emphasized text can be displayed in all sorts of ways aside from being italicized \(e.g., in a different font, a different color, or a bigger size\). Same for `<b>` and`<strong>`.

### empty html elements

HTML condenses consecutive spaces, tabs, or newlines \(together known as “whitespace”\) into a single space. To see what we’re talking about, add the following section to our `basics.html` file:

```markup
<h2>Empty Elements</h2>

<p>Thanks for reading! Interneting should be getting easier now.</p>

<p>Regards,
The Authors</p>
```

The newline after `Regards` in the above snippet will be transformed into a space instead of displaying as a line break:

![Web page showing a plaintext line break collapsing into a space in the rendered page](https://internetingishard.com/html-and-css/basic-web-pages/html-collapsing-whitespace-c4012d.png)

To tell the browser that we want a hard line break, we need to use an explicit `<br/>` element, like this:

```markup
<p>Regards,<br/>
The Authors</p>
```

The `<br/>` element is useful anywhere text formatting matters. Haiku, music lyrics, and signatures are just a few examples where it might come in handy.

![Web page highlighting an actual line break with the &amp;lt;br/&amp;gt; element](https://internetingishard.com/html-and-css/basic-web-pages/html-line-break-element-f40443.png)

However, be very careful not to abuse the `<br/>` tag. Each one you use should still convey _meaning_—you shouldn’t use it to, say, add a bunch of space between paragraphs:

```markup
<!-- (You will be shunned for this) -->
<p>This paragraph needs some space below it...</p>
<br/><br/><br/><br/><br/><br/><br/><br/>
<p>So, I added some hard line breaks.</p>
```

#### horizontal rules <a id="horizontal-rules"></a>



The `<hr/>` element is a “horizontal rule”, which represents a thematic break. The transition from one scene of a story into the next or between the end of a letter and a postscript are good examples of when a horizontal rule may be appropriate. For instance:

```markup
<h2>Empty Elements</h2>

<p>Thanks for reading! Interneting should be getting easier now.</p>

<p>Regards,<br/>
The Authors</p>

<hr/>

<p>P.S. This page might look like crap, but we'll fix that with some CSS
soon.</p>
```

![](../../.gitbook/assets/image%20%2811%29.png)

#### optional trailing slash <a id="optional-trailing-slash"></a>

The trailing slash \(`/`\) in all empty HTML elements is entirely optional. The above snippet could also be marked up like this \(note the lack of `/` in the `<br>` and `<hr>` tags\):

```markup
<p>Regards,<br>
The Authors</p>

<hr>
```

It doesn’t really make a difference which convention you choose, but pick one and stick to it for the sake of consistency. 



