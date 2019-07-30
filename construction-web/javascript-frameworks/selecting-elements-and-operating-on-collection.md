# Selecting elements

Borrowing from CSS 1–3, and then adding its own, jQuery offers a powerful set of tools for matching a set of elements in a document.

To use any of the meta-characters \( such as  ``!"#$%&'()*+,./:;<=>?@[\]^`{|}~`` \) as a literal part of a name, it must be escaped with with two backslashes: `\\`. For example, an element with `id="foo.bar"`, can use the selector `$("#foo\\.bar")`.

### [All Selector \(“\*”\)](https://api.jquery.com/all-selector/)

Selects all elements.

### [:animated Selector](https://api.jquery.com/animated-selector/)

Select all elements that are in the progress of an animation at the time the selector is run.

### [Attribute Contains Prefix Selector \[name\|=”value”\]](https://api.jquery.com/attribute-contains-prefix-selector/)

Selects elements that have the specified attribute with a value either equal to a given string or starting with that string followed by a hyphen \(-\).

### [Attribute Contains Selector \[name\*=”value”\]](https://api.jquery.com/attribute-contains-selector/)

Selects elements that have the specified attribute with a value containing a given substring.

### [Attribute Contains Word Selector \[name~=”value”\]](https://api.jquery.com/attribute-contains-word-selector/)

Selects elements that have the specified attribute with a value containing a given word, delimited by spaces.

### [Attribute Ends With Selector \[name$=”value”\]](https://api.jquery.com/attribute-ends-with-selector/)

Selects elements that have the specified attribute with a value ending exactly with a given string. The comparison is case sensitive.

### [Attribute Equals Selector \[name=”value”\]](https://api.jquery.com/attribute-equals-selector/)

Selects elements that have the specified attribute with a value exactly equal to a certain value.

### [Attribute Not Equal Selector \[name!=”value”\]](https://api.jquery.com/attribute-not-equal-selector/)

Select elements that either don’t have the specified attribute, or do have the specified attribute but not with a certain value.

### [Attribute Starts With Selector \[name^=”value”\]](https://api.jquery.com/attribute-starts-with-selector/)

Selects elements that have the specified attribute with a value beginning exactly with a given string.

### [:button Selector](https://api.jquery.com/button-selector/)

Selects all button elements and elements of type button.

### [:checkbox Selector](https://api.jquery.com/checkbox-selector/)

Selects all elements of type checkbox.

### [:checked Selector](https://api.jquery.com/checked-selector/)

Matches all elements that are checked or selected.

###  [Child Selector \(“parent &gt; child”\)](https://api.jquery.com/child-selector/)

Selects all direct child elements specified by “child” of elements specified by “parent”.

### [Class Selector \(“.class”\)](https://api.jquery.com/class-selector/)

Selects all elements with the given class.

### [:contains\(\) Selector](https://api.jquery.com/contains-selector/)

Select all elements that contain the specified text.

### [Descendant Selector \(“ancestor descendant”\)](https://api.jquery.com/descendant-selector/)

Selects all elements that are descendants of a given ancestor.

### [:disabled Selector](https://api.jquery.com/disabled-selector/)

Selects all elements that are disabled.

### [Element Selector \(“element”\)](https://api.jquery.com/element-selector/)

Selects all elements with the given tag name.

### [:empty Selector](https://api.jquery.com/empty-selector/)

Select all elements that have no children \(including text nodes\).

### [:enabled Selector](https://api.jquery.com/enabled-selector/)

Selects all elements that are enabled.

### [:eq\(\) Selector](https://api.jquery.com/eq-selector/)

Select the element at index n within the matched set.

### [:even Selector](https://api.jquery.com/even-selector/)

Selects even elements, zero-indexed. See also odd.

### [:file Selector](https://api.jquery.com/file-selector/)

Selects all elements of type file.

### [:first-child Selector](https://api.jquery.com/first-child-selector/)

Selects all elements that are the first child of their parent.

### [:first-of-type Selector](https://api.jquery.com/first-of-type-selector/)

Selects all elements that are the first among siblings of the same element name.

### [:first Selector](https://api.jquery.com/first-selector/)

Selects the first matched DOM element.

### [:focus Selector](https://api.jquery.com/focus-selector/)

Selects element if it is currently focused.

### [:gt\(\) Selector](https://api.jquery.com/gt-selector/)

Select all elements at an index greater than index within the matched set.

### [Has Attribute Selector \[name\]](https://api.jquery.com/has-attribute-selector/)

Selects elements that have the specified attribute, with any value.

### [:has\(\) Selector](https://api.jquery.com/has-selector/)

Selects elements which contain at least one element that matches the specified selector.

### [:header Selector](https://api.jquery.com/header-selector/)

Selects all elements that are headers, like h1, h2, h3 and so on.

### [:hidden Selector](https://api.jquery.com/hidden-selector/)

Selects all elements that are hidden.

### [ID Selector \(“\#id”\)](https://api.jquery.com/id-selector/)

Selects a single element with the given id attribute.

### [:image Selector](https://api.jquery.com/image-selector/)

Selects all elements of type image.

### [:input Selector](https://api.jquery.com/input-selector/)

Selects all input, textarea, select and button elements.

### [:lang\(\) Selector](https://api.jquery.com/lang-selector/)

Selects all elements of the specified language.

### [:last-child Selector](https://api.jquery.com/last-child-selector/)

Selects all elements that are the last child of their parent.

### [:last-of-type Selector](https://api.jquery.com/last-of-type-selector/)

Selects all elements that are the last among siblings of the same element name.

### [:last Selector](https://api.jquery.com/last-selector/)

Selects the last matched element.

### [:lt\(\) Selector](https://api.jquery.com/lt-selector/)

Select all elements at an index less than index within the matched set.

### [Multiple Attribute Selector \[name=”value”\]\[name2=”value2″\]](https://api.jquery.com/multiple-attribute-selector/)

Matches elements that match all of the specified attribute filters.

### [Multiple Selector \(“selector1, selector2, selectorN”\)](https://api.jquery.com/multiple-selector/)

Selects the combined results of all the specified selectors.

### [Next Adjacent Selector \(“prev + next”\)](https://api.jquery.com/next-adjacent-selector/)

Selects all next elements matching “next” that are immediately preceded by a sibling “prev”.

### [Next Siblings Selector \(“prev ~ siblings”\)](https://api.jquery.com/next-siblings-selector/)

Selects all sibling elements that follow after the “prev” element, have the same parent, and match the filtering “siblings” selector.

### [:not\(\) Selector](https://api.jquery.com/not-selector/)

Selects all elements that do not match the given selector.

### [:nth-child\(\) Selector](https://api.jquery.com/nth-child-selector/)

Selects all elements that are the nth-child of their parent.

### [:nth-last-child\(\) Selector](https://api.jquery.com/nth-last-child-selector/)

Selects all elements that are the nth-child of their parent, counting from the last element to the first.

### [:nth-last-of-type\(\) Selector](https://api.jquery.com/nth-last-of-type-selector/)

Selects all the elements that are the nth-child of their parent in relation to siblings with the same element name, counting from the last element to the first.

### [:nth-of-type\(\) Selector](https://api.jquery.com/nth-of-type-selector/)

Selects all elements that are the nth child of their parent in relation to siblings with the same element name.

### [:odd Selector](https://api.jquery.com/odd-selector/)

Selects odd elements, zero-indexed. See also even.

### [:only-child Selector](https://api.jquery.com/only-child-selector/)

Selects all elements that are the only child of their parent.

### [:only-of-type Selector](https://api.jquery.com/only-of-type-selector/)

Selects all elements that have no siblings with the same element name.

### [:parent Selector](https://api.jquery.com/parent-selector/)

Select all elements that have at least one child node \(either an element or text\).

### [:password Selector](https://api.jquery.com/password-selector/)

Selects all elements of type password.

### [:radio Selector](https://api.jquery.com/radio-selector/)

Selects all elements of type radio

### [:reset Selector](https://api.jquery.com/reset-selector/)

Selects all elements of type reset.

### [:root Selector](https://api.jquery.com/root-selector/)

Selects the element that is the root of the document.

### [:selected Selector](https://api.jquery.com/selected-selector/)

Selects all elements that are selected.

### [:submit Selector](https://api.jquery.com/submit-selector/)

Selects all elements of type submit.

### [:target Selector](https://api.jquery.com/target-selector/)

Selects the target element indicated by the fragment identifier of the document’s URI.

### [:text Selector](https://api.jquery.com/text-selector/)

Selects all input elements of type text.

### [:visible Selector](https://api.jquery.com/visible-selector/)

Selects all elements that are visible.

