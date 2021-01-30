# ThinQuery

![npm](https://img.shields.io/npm/v/thinquery)

ThinQuery (TQ) is an extremely lightweight Javascript library to make simple queries
of the DOM easier to write. It also includes some curried convenience functions
to make applying a change over many elements simpler.

TQ works best with ES5, as `map` is very powerful when combined with the
curried utilities TQ offers.

Methods of a TQ context do not need to be bound, as they do not rely on `this`.

I mostly just created this for myself because I got tired of writing similar
code over and over but don't want to pull in a dependency like jQuery, but if
you want to see a feature added, feel free to make an issue or pull request and
I'll take a look.

# Examples

The following examples refer to this document:

```html
<div id="box">
    <span class="text-box first" data-description="a description">
        Text box content
    </span>
    <span class="text-box second" data-description="more descriptiveness">
        Another text box content
    </span>
</div>
```

```javascript
import { ThinQuery } from 'thinquery';

// Get ThinQuery context
const $ = new ThinQuery(document)

// getElementById
const box = $.id("box")

// getElementsByClassName, but returns an array
const textBoxes = $.class("text-box")

// querySelector
const firstTextBox = $.select(".first.text-box")

// querySelectorAll
const boxChildren = $.selectAll("#box span")

// gets the attribute of each element
const descriptions = textBoxes.map($.getAttribute("data-description"))

// modifies the `style` property of each element

textBoxes.forEach(
    $.addCss({
        color: "blue",
        backgroundColor: "yellow"
    })
)
```

# Full Function List

```javascript
// given $ is a ThinQuery context returned by thinQuery...

// gets an element by its id
$.id(id)

// gets an array of elements with the specified class name
$.class(className)

// gets the first element that matches the specified CSS selector
$.select(selector)

// gets an array of elements that match the selector
$.selectAll(selector)

// adds the class to the element. Best used in higher-order functions like forEach
$.addClass(className)(element)

// removes the class from the element. Best used in higher-order functions like forEach
$.removeClass(className)(element)

// adds the CSS to the element, using an object. Keys are CSS style property
// names, values are the corresponding values. Best used in higher-order functions
// like forEach
$.addCss(cssObj)(element)

// sets the specified attribute. Best used in higher-order functions like
// forEach
$.setAttribute(name, value)(element)

// gets the specified attribute. Best used in higher-order functions like map
$.getAttribute(name)(element)

// sets the textContent of the element. Best used in higher-order functions like
// forEach
$.setText(text)(element)

// gets the textContent of the element. Best used in higher-order functions like
// map
$.getText(element)

// sets the `value`attribute of the element. Best used in higher-order functions like
// forEach
$.setValue(val)(element)

// gets the `value`attribute of the element. Best used in higher-order functions like
// map
$.getValue(element)
```
