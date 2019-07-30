# JavaScript: JS in WebBrowser and basic DOM manipulations

Client-side JavaScript code is embedded within HTML documents in four ways: 

* Inline, between a pair of  and  tags 
* From an external file specified by the src attribute of a  tag  

```markup
<script src="../../scripts/util.js"></script>
```

* In an HTML event handler attribute, such as onclick or onmouseover 

```markup
<input type="checkbox" name="options" value="giftwrap"
 onchange="order.options.giftwrap = this.checked;">
```

* In a URL that uses the special javascript: protocol.

```markup
<a href="javascript:new Date().toLocaleTimeString();">
What time is it?
</a>
```

The Document Object Model, or DOM, is the fundamental API for representing and manipulating the content of HTML and XML documents. The API is not particularly complicated, but there are a number of architectural details you need to understand. First, you should understand that the nested elements of an HTML or XML document are represented in the DOM as a tree of objects. The tree representation of an HTML document contains nodes representing HTML tags or elements, such as and

, and nodes representing strings of text. An HTML document may also contain nodes representing HTML comments. Consider the following simple HTML document:

```markup
<html>
 <head>
  <title>Sample Document</title>
 </head>
 <body>
  <h1>An HTML Document</h1>
  <p>This is a <i>simple</i> document.
</html>
```

The DOM representation of this document:

![](../../.gitbook/assets/image%20%2891%29.png)

