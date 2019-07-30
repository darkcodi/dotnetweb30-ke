# CSS: Elements positioning and layering

“Static positioning” refers to the normal flow of the page that we’ve been working with up ’til this point. The other three types of positioning are “relative”, “absolute”, and “fixed”.

![](../../.gitbook/assets/image%20%28136%29.png)

The CSS `position` property lets you alter the positioning scheme of a particular element. Its default value, as you might imagine, is `static`. When an element’s `position` property _doesn’t_ have a value of `static`, it’s called a “positioned element”. Positioned elements are what this entire chapter is about.

![Diagram: relative, absolute, and fixed elements denoted as positioned elements](https://internetingishard.com/html-and-css/advanced-positioning/positioned-elements-terminology-861fca.png)

### relative positioning

“Relative positioning” moves elements around _relative_ to where they would normally appear in the static flow of the page. This is useful for nudging boxes around when the default flow is just a little bit off.

![Diagram: relatively positioned box offset from the upper left corner of its static position](https://internetingishard.com/html-and-css/advanced-positioning/css-relative-positioning-26842e.png)

Let’s turn the `.item-relative` element in `schemes.html` into a relatively positioned element. Add the following rule to `styles.css`:

```css
.item-relative {
  position: relative;
  top: 30px;
  left: 30px;
}
```

The `position: relative;` line makes it a positioned element, and the `top`and `left` properties let you define how far it’s offset from its static position. This is sort of like setting an \(_x_, _y_\) coordinate for the element.

![Web page with a relatively positioned element](https://internetingishard.com/html-and-css/advanced-positioning/relative-positioning-screenshot-4c23c2.png)

Relative positioning works similarly to margins, with one very important difference: neither the surrounding elements or parent element are affected by the `top` and `left` values. Everything else renders as if `.item-relative`was in its original position. Think of the offsets as being applied _after_ the browser finishes laying out the page.

The `top` and `left` properties measure from the original box’s top and left edges, respectively. We can offset relative to the other edges with the `bottom` and `right` properties.

![Diagram: top, left, bottom, and right offsets of a relatively positioned element](https://internetingishard.com/html-and-css/advanced-positioning/relative-positioning-offsets-494268.png)

For example, the following will nudge the box in the opposite direction:

```css
.item-relative {
  position: relative;
  bottom: 30px;
  right: 30px;
}
```

### absolute positioning

“Absolute positioning” is just like relative positioning, but the offset is relative to the entire browser window instead of the original position of the element. Since there’s no longer any relationship with the static flow of the page, consider this the most manual way to lay out an element.

![Diagram: absolutely positioned element offset from the top-left of the browser window](https://internetingishard.com/html-and-css/advanced-positioning/css-absolute-positioning-228ce0.png)

Let’s take a look by adding the following rule to our stylesheet:

```css
.item-absolute {
  position: absolute;
  top: 10px;
  left: 10px;
}
```

Our HTML structure is the exact same as the previous example, but this will stick the purple image in the top-left corner of the browser window. You can also try setting a `bottom` or `right` value to get a clearer idea of what’s going on.

![Web page with an absolutely positioned element](https://internetingishard.com/html-and-css/advanced-positioning/absolute-positioning-screenshot-641ad7.png)

![Web page highlighting the empty space left by an absolutely positioned element](https://internetingishard.com/html-and-css/advanced-positioning/absolute-positioning-flex-start-screenshot-d4b627.png)

This behavior isn’t really all that useful most of the time because it would mean _everything_ on your page needs to be absolutely positioned—otherwise we’d get unpredictable overlaps of static elements with absolute elements. So, why does `absolute` even exist?

### \(relatively\) absolute positioning

Absolute positioning becomes much more practical when it’s relative to some other element that _is_ in the static flow of the page. Fortunately, there’s a way to change the coordinate system of an absolutely positioned element.

![Diagram: absolute element positioned relative to a parent positioned element](https://internetingishard.com/html-and-css/advanced-positioning/css-relatively-absolute-positioning-1ba963.png)

if we change`.item-absolute`’s parent element to be relatively positioned, it should appear in the top-left corner of _that_ element instead of the browser window.

```css
.absolute {
  position: relative;
}
```

The `.absolute` div is laid out with the normal flow of the page, and we can manually move around our `.item-absolute` wherever we need to. This is great, because if we want to alter the normal flow of the container, say, for a mobile layout, any absolutely positioned elements will automatically move with it.

![Web page with an absolutely positioned element inside another element that is relatively positioned](https://internetingishard.com/html-and-css/advanced-positioning/relatively-absolute-positioning-screenshot-98bcce.png)

Notice how we didn’t specify any offset coordinates for `.absolute`. We’re using relative positioning for the sole purpose of letting our absolute element hook back into the normal flow of the page. This is how we safely combine absolute positioning with static positioning.

### fixed positioning

“Fixed positioning” has a lot in common with absolute positioning: it’s very manual, the element is removed from the normal flow of the page, and the coordinate system is relative to the entire browser window. The key difference is that fixed elements don’t scroll with the rest of the page.

![Diagram: fixed element positioned relative to the browser window, but with scrolling disabled](https://internetingishard.com/html-and-css/advanced-positioning/css-fixed-positioning-342eff.png)

Go ahead and update our third example to use fixed positioning:

```css
.item-fixed {
  position: fixed;
  bottom: 0;
  right: 0;
}
```

This will place the red image in the bottom-right corner of the screen. Try scrolling the page, and you’ll discover that it doesn’t move with the rest of the elements on the page, while the absolutely positioned purple image does.

This lets you create navigation bars that always stay on the screen, as well as those annoying pop-up banners that never go away.

### summary

Relative positioning was for tweaking the position of an element without affecting its surrounding boxes. Absolute positioning took elements out of the static flow of the page and placed them relative to the browser window, while relatively absolute positioning allowed us to hook back into the static flow of the page. Finally, fixed positioning let us make elements that didn't scroll with the rest of the page.

![Diagram: comparison of relative, absolute, relatively absolute, and fixed positioning schemes](https://internetingishard.com/html-and-css/advanced-positioning/css-positioning-schemes-summary-d7f831.png)

