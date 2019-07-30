# CSS: selectors

![Diagram: CSS selector connecting a CSS rule to an HTML element](https://internetingishard.com/html-and-css/css-selectors/css-selectors-1f0064.png)

Unless you want every section of your website to look exactly the same, this is a crucial bit of functionality for us. It’s how we say things like “I want this paragraph to be blue and that other paragraph to be yellow.” Until now, we’ve only been able to turn _all_ our paragraphs blue \(or yellow\).

### class selectors

“Class selectors” let you apply CSS styles to a specific HTML element. They let you differentiate between HTML elements of the same type.

Class selectors require two things:

* A `class` attribute on the HTML element in question.
* A matching CSS class selector in your stylesheet.

![Diagram: CSS class selector connecting a CSS rule to a class attribute on an HTML element](https://internetingishard.com/html-and-css/css-selectors/class-selector-ce3fd0.png)

First, let’s add a `class` attribute to the desired paragraph:

```markup
<p class='synopsis'>CSS selectors let you <em>select</em> individual HTML
   elements in an HTML document. This is <strong>super</strong> useful.</p>
```

Now, we can pluck out that `<p class='synopsis'>` element in our CSS with the following \(add this to `styles.css`\):

```css
.synopsis {
  color: #7E8184;        /* Light gray */
  font-style: italic;
}
```

This rule is _only_ applied to elements with the corresponding `class` attribute. Notice the dot \(`.`\) prefixing the class name. This distinguishes class selectors from the type selectors that we’ve been working with before this chapter.

### 



