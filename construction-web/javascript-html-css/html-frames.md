# HTML: Frames

### &lt;frameset&gt; Tag

The &lt;frameset&gt; tag is not supported in HTML5.

The &lt;frameset&gt; tag defines a frameset.

The &lt;frameset&gt; element holds one or more [&lt;frame&gt;](https://www.w3schools.com/tags/tag_frame.asp) elements. Each &lt;frame&gt; element can hold a separate document.

```markup
<frameset cols="25%,50%,25%">
  <frame src="frame_a.htm">
  <frame src="frame_b.htm">
  <frame src="frame_c.htm">
</frameset>
```

The &lt;frameset&gt; element specifies HOW MANY columns or rows there will be in the frameset, and HOW MUCH percentage/pixels of space will occupy each of them.

| Attribute | Value | Description |
| :--- | :--- | :--- |
| [cols](https://www.w3schools.com/tags/att_frameset_cols.asp) | pixels % \* | Not supported in HTML5. Specifies the number and size of columns in a frameset |
| [rows](https://www.w3schools.com/tags/att_frameset_rows.asp) | pixels % \* | Not supported in HTML5. Specifies the number and size of rows in a frameset |

### &lt;frame&gt; Tag

The &lt;frame&gt; tag is not supported in HTML5.

The &lt;frame&gt; tag defines one particular window \(frame\) within a &lt;frameset&gt;.

Each &lt;frame&gt; in a &lt;frameset&gt; can have different attributes, such as border, scrolling, the ability to resize, etc.

**Note:** If you want to validate a page containing frames, be sure the [&lt;!DOCTYPE&gt;](https://www.w3schools.com/tags/tag_doctype.asp) is set to either "HTML Frameset DTD" or "XHTML Frameset DTD".



| Attribute | Value | Description |
| :--- | :--- | :--- |
| [frameborder](https://www.w3schools.com/tags/att_frame_frameborder.asp) | 0 1 | Not supported in HTML5. Specifies whether or not to display a border around a frame |
| [longdesc](https://www.w3schools.com/tags/att_frame_longdesc.asp) | URL | Not supported in HTML5. Specifies a page that contains a long description of the content of a frame |
| [marginheight](https://www.w3schools.com/tags/att_frame_marginheight.asp) | pixels | Not supported in HTML5. Specifies the top and bottom margins of a frame |
| [marginwidth](https://www.w3schools.com/tags/att_frame_marginwidth.asp) | pixels | Not supported in HTML5. Specifies the left and right margins of a frame |
| [name](https://www.w3schools.com/tags/att_frame_name.asp) | text | Not supported in HTML5. Specifies the name of a frame |
| [noresize](https://www.w3schools.com/tags/att_frame_noresize.asp) | noresize | Not supported in HTML5. Specifies that a frame is not resizable |
| [scrolling](https://www.w3schools.com/tags/att_frame_scrolling.asp) | yes no auto | Not supported in HTML5. Specifies whether or not to display scrollbars in a frame |
| [src](https://www.w3schools.com/tags/att_frame_src.asp) | URL | Not supported in HTML5. Specifies the URL of the document to show in a frame |

