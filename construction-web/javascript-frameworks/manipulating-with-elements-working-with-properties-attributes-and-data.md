# Manipulating with elements, working with properties, attributes and data

 All of the methods in this section manipulate the DOM in some manner. A few of them simply change one of the attributes of an element \(also listed in the [Attributes category](https://api.jquery.com/category/attributes/)\), while others set an element's style properties \(also listed in the [CSS category](https://api.jquery.com/category/css/)\). Still others modify entire elements \(or groups of elements\) themselves—inserting, copying, removing, and so on. All of these methods are referred to as "setters," as they change the values of properties.  
A few of these methods—such as `.attr()`, `.html()`, and `.val()`—also act as "getters," retrieving information from DOM elements for later use.

### [.addClass\(\)](https://api.jquery.com/addClass/)

Adds the specified class\(es\) to each element in the set of matched elements.

### [.after\(\)](https://api.jquery.com/after/)

Insert content, specified by the parameter, after each element in the set of matched elements.

### [.append\(\)](https://api.jquery.com/append/)

Insert content, specified by the parameter, to the end of each element in the set of matched elements.

### [.appendTo\(\)](https://api.jquery.com/appendTo/)

Insert every element in the set of matched elements to the end of the target.

### [.attr\(\)](https://api.jquery.com/attr/)

Get the value of an attribute for the first element in the set of matched elements or set one or more attributes for every matched element.

### [.before\(\)](https://api.jquery.com/before/)

Insert content, specified by the parameter, before each element in the set of matched elements.

### [.clone\(\)](https://api.jquery.com/clone/)

Create a deep copy of the set of matched elements.

### [.css\(\)](https://api.jquery.com/css/)

Get the value of a computed style property for the first element in the set of matched elements or set one or more CSS properties for every matched element.

### [.detach\(\)](https://api.jquery.com/detach/)

Remove the set of matched elements from the DOM

### [.empty\(\)](https://api.jquery.com/empty/)

Remove all child nodes of the set of matched elements from the DOM.

### [.hasClass\(\)](https://api.jquery.com/hasClass/)

Determine whether any of the matched elements are assigned the given class.

### [.height\(\)](https://api.jquery.com/height/)

Get the current computed height for the first element in the set of matched elements or set the height of every matched element.

### [.html\(\)](https://api.jquery.com/html/)

Get the HTML contents of the first element in the set of matched elements or set the HTML contents of every matched element.

### [.innerHeight\(\)](https://api.jquery.com/innerHeight/)

Get the current computed inner height \(including padding but not border\) for the first element in the set of matched elements or set the inner height of every matched element.

### [.innerWidth\(\)](https://api.jquery.com/innerWidth/)

Get the current computed inner width \(including padding but not border\) for the first element in the set of matched elements or set the inner width of every matched element.

### [.insertAfter\(\)](https://api.jquery.com/insertAfter/)

Insert every element in the set of matched elements after the target.

### [.insertBefore\(\)](https://api.jquery.com/insertBefore/)

Insert every element in the set of matched elements before the target.

### [jQuery.cssNumber](https://api.jquery.com/jQuery.cssNumber/)

An object containing all CSS properties that may be used without a unit. The .css\(\) method uses this object to see if it may append px to unitless values.

### [jQuery.htmlPrefilter\(\)](https://api.jquery.com/jQuery.htmlPrefilter/)

Modify and filter HTML strings passed through jQuery manipulation methods.

### [.offset\(\)](https://api.jquery.com/offset/)

Get the current coordinates of the first element, or set the coordinates of every element, in the set of matched elements, relative to the document.

### [.outerHeight\(\)](https://api.jquery.com/outerHeight/)

Get the current computed outer height \(including padding, border, and optionally margin\) for the first element in the set of matched elements or set the outer height of every matched element.

### [.outerWidth\(\)](https://api.jquery.com/outerWidth/)

Get the current computed outer width \(including padding, border, and optionally margin\) for the first element in the set of matched elements or set the outer width of every matched element.

### [.position\(\)](https://api.jquery.com/position/)

Get the current coordinates of the first element in the set of matched elements, relative to the offset parent.

### [.prepend\(\)](https://api.jquery.com/prepend/)

Insert content, specified by the parameter, to the beginning of each element in the set of matched elements.

### [.prependTo\(\)](https://api.jquery.com/prependTo/)

Insert every element in the set of matched elements to the beginning of the target.

### [.prop\(\)](https://api.jquery.com/prop/)

Get the value of a property for the first element in the set of matched elements or set one or more properties for every matched element.

### [.remove\(\)](https://api.jquery.com/remove/)

Remove the set of matched elements from the DOM.

### [.removeAttr\(\)](https://api.jquery.com/removeAttr/)

Remove an attribute from each element in the set of matched elements.

### [.removeClass\(\)](https://api.jquery.com/removeClass/)

Remove a single class, multiple classes, or all classes from each element in the set of matched elements.

### [.removeProp\(\)](https://api.jquery.com/removeProp/)

Remove a property for the set of matched elements.

### [.replaceAll\(\)](https://api.jquery.com/replaceAll/)

Replace each target element with the set of matched elements.

### [.replaceWith\(\)](https://api.jquery.com/replaceWith/)

Replace each element in the set of matched elements with the provided new content and return the set of elements that was removed.

### [.scrollLeft\(\)](https://api.jquery.com/scrollLeft/)

Get the current horizontal position of the scroll bar for the first element in the set of matched elements or set the horizontal position of the scroll bar for every matched element.

### [.scrollTop\(\)](https://api.jquery.com/scrollTop/)

Get the current vertical position of the scroll bar for the first element in the set of matched elements or set the vertical position of the scroll bar for every matched element.

### [.text\(\)](https://api.jquery.com/text/)

Get the combined text contents of each element in the set of matched elements, including their descendants, or set the text contents of the matched elements.

### [.toggleClass\(\)](https://api.jquery.com/toggleClass/)

Add or remove one or more classes from each element in the set of matched elements, depending on either the class’s presence or the value of the state argument.

### [.unwrap\(\)](https://api.jquery.com/unwrap/)

Remove the parents of the set of matched elements from the DOM, leaving the matched elements in their place.

### [.val\(\)](https://api.jquery.com/val/)

Get the current value of the first element in the set of matched elements or set the value of every matched element.

### [.width\(\)](https://api.jquery.com/width/)

Get the current computed width for the first element in the set of matched elements or set the width of every matched element.

### [.wrap\(\)](https://api.jquery.com/wrap/)

Wrap an HTML structure around each element in the set of matched elements.

### [.wrapAll\(\)](https://api.jquery.com/wrapAll/)

Wrap an HTML structure around all elements in the set of matched elements.

### [.wrapInner\(\)](https://api.jquery.com/wrapInner/)

Wrap an HTML structure around the content of each element in the set of matched elements.

