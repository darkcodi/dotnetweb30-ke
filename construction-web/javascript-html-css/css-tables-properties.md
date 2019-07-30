# CSS: Tables properties

### Table Borders

To specify table borders in CSS, use the `border` property.

The example below specifies a black border for &lt;table&gt;, &lt;th&gt;, and &lt;td&gt; elements:

```css
table, th, td {
  border: 1px solid black;
}
```

Notice that the table in the example above has double borders. This is because both the table and the &lt;th&gt; and &lt;td&gt; elements have separate borders.

### Collapse Table Borders

The `border-collapse` property sets whether the table borders should be collapsed into a single border:

```css
table {
  border-collapse: collapse;
}

table, th, td {
  border: 1px solid black;
}
```

If you only want a border around the table, only specify the `border` property for &lt;table&gt;:

```css
table {
  border: 1px solid black;
}
```

### Table Width and Height

Width and height of a table are defined by the `width` and `height` properties.

The example below sets the width of the table to 100%, and the height of the &lt;th&gt; elements to 50px:

```css
table {
  width: 100%;
}

th {
  height: 50px;
}
```

### Horizontal Alignment

The `text-align` property sets the horizontal alignment \(like left, right, or center\) of the content in &lt;th&gt; or &lt;td&gt;.

By default, the content of &lt;th&gt; elements are center-aligned and the content of &lt;td&gt; elements are left-aligned.

The following example left-aligns the text in &lt;th&gt; elements:

```css
th {
  text-align: left;
}
```

### Vertical Alignment

The `vertical-align` property sets the vertical alignment \(like top, bottom, or middle\) of the content in &lt;th&gt; or &lt;td&gt;.

By default, the vertical alignment of the content in a table is middle \(for both &lt;th&gt; and &lt;td&gt; elements\).

The following example sets the vertical text alignment to bottom for &lt;td&gt; elements:

```css
td {
  height: 50px;
  vertical-align: bottom;
}
```

### Table Padding

To control the space between the border and the content in a table, use the `padding` property on &lt;td&gt; and &lt;th&gt; elements:

```css
th, td {
  padding: 15px;
  text-align: left;
}
```

### Horizontal Dividers

| First Name | Last Name | Savings |
| :--- | :--- | :--- |
| Peter | Griffin | $100 |
| Lois | Griffin | $150 |
| Joe | Swanson | $300 |

Add the `border-bottom` property to &lt;th&gt; and &lt;td&gt; for horizontal dividers:

```css
th, td {
  border-bottom: 1px solid #ddd;
}
```

### Hoverable Table

Use the `:hover` selector on &lt;tr&gt; to highlight table rows on mouse over:

| First Name | Last Name | Savings |
| :--- | :--- | :--- |
| Peter | Griffin | $100 |
| Lois | Griffin | $150 |
| Joe | Swanson | $300 |

```css
tr:hover {background-color: #f5f5f5;}
```

### Striped Tables

| First Name | Last Name | Savings |
| :--- | :--- | :--- |
| Peter | Griffin | $100 |
| Lois | Griffin | $150 |
| Joe | Swanson | $300 |

For zebra-striped tables, use the `nth-child()` selector and add a `background-color` to all even \(or odd\) table rows:

```css
tr:nth-child(even) {background-color: #f2f2f2;}
```

### Table Color

The example below specifies the background color and text color of &lt;th&gt; elements:

| First Name | Last Name | Savings |
| :--- | :--- | :--- |
| Peter | Griffin | $100 |
| Lois | Griffin | $150 |
| Joe | Swanson | $300 |

```css
th {
  background-color: #4CAF50;
  color: white;
}
```

### Responsive Table

A responsive table will display a horizontal scroll bar if the screen is too small to display the full content:

| First Name | Last Name | Points | Points | Points | Points | Points | Points | Points | Points | Points | Points | Points | Points |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Jill | Smith | 50 | 50 | 50 | 50 | 50 | 50 | 50 | 50 | 50 | 50 | 50 | 50 |
| Eve | Jackson | 94 | 94 | 94 | 94 | 94 | 94 | 94 | 94 | 94 | 94 | 94 | 94 |
| Adam | Johnson | 67 | 67 | 67 | 67 | 67 | 67 | 67 | 67 | 67 | 67 | 67 | 67 |

Add a container element \(like &lt;div&gt;\) with `overflow-x:auto` around the &lt;table&gt; element to make it responsive:

```text
<div style="overflow-x:auto;">

<table>
... table content ...
</table>

</div>
```

**Note:** In OS X Lion \(on Mac\), scrollbars are hidden by default and only shown when being used \(even though "overflow:scroll" is set\).

