# CSS: Flexbox

The “Flexible Box” or “Flexbox” layout mode offers an alternative to [Floats](https://internetingishard.com/html-and-css/floats/)for defining the overall appearance of a web page. Whereas floats only let us horizontally position our boxes, flexbox gives us _complete_ control over the alignment, direction, order, and size of our boxes.

![Diagram: comparison of flexbox alignment, direction, order, and size properties](https://internetingishard.com/html-and-css/flexbox/flexbox-layouts-7abd58.png)

![Diagram: CSS floats for text wrapping around a box versus flexbox for the rest of the page layout](https://internetingishard.com/html-and-css/flexbox/flexbox-vs-floats-418bf3.png)

### flexbox overview

Flexbox uses two types of boxes that we’ve never seen before: “flex containers” and “flex items”. The job of a flex container is to group a bunch of flex items together and define how they’re positioned.

![Diagram: flex container as a highlighted container wrapping grayed out elements versus flex items as highlighted boxes inside the container](https://internetingishard.com/html-and-css/flexbox/flex-container-and-flex-items-6234bb.png)

### flex containers

```css
.menu-container {
  /* ... */
  display: flex;
}
```

This _enables_ the flexbox layout mode—without it, the browser would ignore all the flexbox properties that we’re about to introduce. Explicitly defining flex containers means that you can mix and match flexbox with other layout models \(e.g., floats and everything we’re going to learn in [Advanced Positioning](https://internetingishard.com/html-and-css/advanced-positioning/)\).

![Diagram: Mixing and matching flexbox layout with block boxes and floats](https://internetingishard.com/html-and-css/flexbox/enabling-flexbox-dd3b59.png)

### aligning a flex item

After you’ve got a flex container, your next job is to define the horizontal alignment of its items.



```text
.menu-container {
  /* ... */
  display: flex;
  justify-content: center;    /* Add this */
}
```

This has the same effect as adding a `margin: 0 auto` declaration to the `.menu` element. But, notice how we did this by adding a property to the _parent_ element \(the flex container\) instead of directly to the element we wanted to center \(the flex item\). Manipulating items through their containers like this is a common theme in flexbox, and it’s a bit of a divergence from how we’ve been positioning boxes thus far.

![Diagram: flex-start \(3 left-aligned boxes\), center \(3 center-aligned boxes\), flex-end \(3 right-aligned boxes\)](https://internetingishard.com/html-and-css/flexbox/flex-justify-content-alignment-ea129c.png)

Other values for `justify-content` are shown below:

* `center`
* `flex-start`
* `flex-end`
* `space-around`
* `space-between`

Try changing `justify-content` to `flex-start` and `flex-end`. This should align the menu to the left and right side of the browser window, respectively. Be sure to change it back to `center` before moving on. The last two options are only useful when you have multiple flex items in a container.

### grouping flex items

Flex containers only know how to position elements that are one level deep \(i.e., their child elements\). They don’t care one bit about what’s inside their flex items. This means that grouping flex items is another weapon in your layout-creation arsenal. Wrapping a bunch of items in an extra `<div>`results in a totally different web page.

![Diagram: wrapping two flex items in a &amp;lt;div&amp;gt; to eliminate one of the flex items](https://internetingishard.com/html-and-css/flexbox/grouping-flex-items-1bb642.png)

```css
<div class='menu'>
  <div class='date'>Aug 14, 2016</div>
  <div class='links'>
    <div class='signup'>Sign Up</div>      <!-- This is nested now -->
    <div class='login'>Login</div>         <!-- This one too! -->
  </div>
</div>
```

![](../../.gitbook/assets/image%20%2847%29.png)

```css
.links {
  border: 1px solid #fff;  /* For debugging */
  display: flex;
  justify-content: flex-end;
}

.login {
  margin-left: 20px;
}
```

![](../../.gitbook/assets/image%20%2842%29.png)

### cross-axis \(vertical\) alignment

his is something that’s simply not possible with floats.

![Diagram: justify-content \(left and right\), align-items \(top and bottom\)](https://internetingishard.com/html-and-css/flexbox/align-items-vs-justify-content-4d380e.png)

The available options for `align-items` is similar to `justify-content`:

* `center`
* `flex-start`   \(top\)
* `flex-end`      \(bottom\)
* `stretch`
* `baseline`

![Diagram: flex-start \(boxes at top of container\), center \(boxes in center of container\), flex-end \(boxes at bottom of container, stretch \(boxes filling height of container\)](https://internetingishard.com/html-and-css/flexbox/flex-align-items-26abfd.png)

Most of these are pretty straightforward. The `stretch` option is worth a taking a minute to play with because it lets you display the background of each element. Let’s take a brief look by adding the following to `styles.css`:

```css
.header {
  /* ... */
  align-items: stretch;    /* Change this */
}
```

### wrapping flex items

To create a grid, we need the `flex-wrap` property.

![Diagram: no wrapping \(boxes flowing outside of container\), with wrapping \(boxes wrapping to next line in container\)](https://internetingishard.com/html-and-css/flexbox/flex-wrap-b960c1.png)

![](../../.gitbook/assets/image%20%2833%29.png)

```css
.photo-grid {
  /* ... */
  flex-wrap: wrap;
}
```

![](../../.gitbook/assets/image%20%2814%29.png)

### flex container direction

“Direction” refers to whether a container renders its items horizontally or vertically. So far, all the containers we’ve seen use the default horizontal direction, which means items are drawn one after another in the same row before popping down to the next column when they run out of space.

![Diagram: row \(3 horizontal boxes\), column \(3 vertical boxes\)](https://internetingishard.com/html-and-css/flexbox/flex-direction-9acadf.png)

Try adding the following`flex-direction` declaration to our `.photo-grid` rule:

```css
.photo-grid {
  /* ... */
  flex-direction: column;
}
```

![](../../.gitbook/assets/image%20%2872%29.png)

#### alignment considerations <a id="alignment-considerations"></a>

Notice that the column is hugging the left side of its flex container despite our `justify-content: center;` declaration. When you rotate the direction of a container, you also rotate the direction of the `justify-content`property. It now refers to the container’s vertical alignment—not its horizontal alignment.

![Diagram: axes flipped when flex-direction is equal to column](https://internetingishard.com/html-and-css/flexbox/flex-direction-axes-b30e85.png)

To horizontally center our column, we need to define an `align-items`property on our `.photo-grid`:

```css
.photo-grid {
  /* ... */
  flex-direction: column;
  align-items: center;      /* Add this */
}
```

### flex container order

![Diagram: row \(left to right\), row-reverse \(right to left\), column \(top to bottom\), column-reverse \(bottom to top\)](https://internetingishard.com/html-and-css/flexbox/flex-direction-reverse-532d8f.png)

The `flex-direction` property also offers you control over the order in which items appear via the `row-reverse` and `column-reverse` properties. 

![](../../.gitbook/assets/image%20%2892%29.png)

### flex item order

This entire chapter has been about positioning flex items _through their parent containers_, but it’s also possible to manipulate individual items. The rest of this chapter is going to shift focus away from flex containers onto the items they contain.

![Diagram: setting the order of a flex item individual with the order property](https://internetingishard.com/html-and-css/flexbox/flex-direction-vs-order-021cee.png)

### flex item alignment

We can do the same thing with vertical alignment. What if we want that**Subscribe** link and those social icons to go at the bottom of the header instead of the center? Align them individually! This is where the `align-self` property comes in. Adding this to a flex item overrides the `align-items` value from its container:

```css
.social,
.subscribe {
  align-self: flex-end;
  margin-bottom: 20px;
}
```

This should send them to the bottom of the `.header`. Note that margins \(padding, too\) work just like you’d expect.

![Web page showing bottom-aligned icons via the align-self property](https://internetingishard.com/html-and-css/flexbox/grid-align-self-4302c2.png)

You can align elements in other ways using the same values as the `align-items` property, listed below for convenience.

* `center`
* `flex-start`   \(top\)
* `flex-end`      \(bottom\)
* `stretch`
* `baseline`

### flexible items

Flex items are _flexible_: they can shrink and stretch to match the width of their containers.

The `flex` property defines the width of individual items in a flex container. Or, more accurately, it allows them to have flexible widths. It works as a weight that tells the flex container how to distribute extra space to each item. For example, an item with a `flex` value of `2` will grow twice as fast as items with the default value of `1`.

![Diagram: no flex \(3 square boxes\), equal flex \(3 rectangle boxes\), unequal flex \(2 smaller boxes, one stretched out box\)](https://internetingishard.com/html-and-css/flexbox/flexible-items-cfe7a3.png)

```css
.footer {
  display: flex;
  justify-content: space-between;
}

.footer-item {
  border: 1px solid #fff;
  background-color: #D6E9FE;
  height: 200px;
  flex: 1;
}
```

That `flex: 1;` line tells the items to stretch to match the width of `.footer`. Since they all have the same weight, they’ll stretch equally:

![Web page with three equal boxes that stretch to fill the footer](https://internetingishard.com/html-and-css/flexbox/footer-flexible-items-220ac8.png)

Increasing the weight of one of the items makes it grow faster than the others. For example, we can make the third item grow twice as fast as the other two with the following rule:

```css
.footer-three {
  flex: 2;
}
```

Compare this to the `justify-content` property, which distributes extra space _between_ items. This is similar, but now we’re distributing that space into the items themselves. The result is full control over how flex items fit into their containers.

### static item widths

We can even mix-and-match flexible boxes with fixed-width ones. `flex: initial` falls back to the item’s explicit `width` property. This lets us combine static and flexible boxes in complex ways.

![Diagram: fixed-width box \(flex: initial\), flexible box \(flex: 1\)](https://internetingishard.com/html-and-css/flexbox/combining-flexible-and-static-items-52aacb.png)

We’re going to make our footer behave like the above diagram. The center item is flexible, but the ones on either side are always the same size. All we need to do is add the following rule to our stylesheet:

```css
.footer-one,
.footer-three {
  background-color: #5995DA;
  flex: initial;
  width: 300px;
}
```

![](../../.gitbook/assets/image%20%2821%29.png)

### summary

* Use `display: flex;` to create a flex container.
* Use `justify-content` to define the horizontal alignment of items.
* Use `align-items` to define the vertical alignment of items.
* Use `flex-direction` if you need columns instead of rows.
* Use the `row-reverse` or `column-reverse` values to flip item order.
* Use `order` to customize the order of individual elements.
* Use `align-self` to vertically align individual items.
* Use `flex` to create flexible boxes that can stretch and shrink.

