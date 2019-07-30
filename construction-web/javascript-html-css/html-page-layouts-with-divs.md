# HTML: Page Layouts with divs

The traditional way of positioning HTML elements was to place them inside invisible tables. But this was complicated to do and caused web pages to load very slowly. Not only that, but it is now officially the **wrong** way to do it!

The new, official way to lay out our page elements is using CSS. It can do everything tables can do and much more, and as an added bonus it loads a heck of a lot faster than tables ever did. To people who are used to laying their web pages out using HTML tables it can seem a bit daunting, but in fact it is a much more intuitive way of doing things.

Before we can set about positioning our HTML elements using CSS, we need to define the various different sections of our web page. We do this using `<div>` tags. The following example gives a typical example of how we might define a web page with a header, a side menu and some content:

```markup
<div id="header"> ...header text goes here... </div>
<div id="menu"> ...menu links goes in here... </div>
<div id="content"> ...and finally page content in here... </div>
```

As you can see, we have used `<div>` tags to define the three areas of our page, and within those divisions we can place anything we want - text, pictures, links etc.

### Default &lt;div&gt; layout

As it stands we have simply defined various sections of our HTML, but we haven't begun to adjust the layout yet. `divs` are block-level elements. This means that they will automatically fill 100% of the available page width, and our sections will line up one beneath the other. On the next page we will begin to write the CSS to position our elements exactly where we want them.

