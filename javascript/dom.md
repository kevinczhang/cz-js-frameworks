---
description: Document Object Model
---

# DOM

When a web page is loaded, the browser creates a **D**ocument **O**bject **M**odel of the page. With the HTML DOM, JavaScript can access and change all the elements of an HTML document.

The **HTML DOM** model is constructed as a tree of **Objects**:

![The HTML DOM Tree of Objects](../.gitbook/assets/image%20%283%29.png)

Window object - The Browser Object Model

The window object represents a window in browser. An object of window is created automatically by the browser. Window is the object of browser, it is not the object of javascript. The javascript objects are string, array, date etc.

The Browser Object Model \(BOM\) allows JavaScript to "talk to" the browser. All global JavaScript objects, functions, and variables automatically become members of the window object. Global variables are properties of the window object. Global functions are methods of the window object. Even the document object \(of the HTML DOM\) is a property of the window object

* The window.screen object contains information about the user's screen.
*  The `window.location` object can be used to get the current page address \(URL\) and to redirect the browser to a new page.
*  The `window.history` object contains the browsers history.
*  The `window.navigator` object contains information about the visitor's browser.

### Finding HTML Elements

| Method | Description |
| :--- | :--- |
| document.getElementById\(_id_\) | Find an element by element id |
| document.getElementsByTagName\(_name_\) | Find elements by tag name |
| document.getElementsByClassName\(_name_\) | Find elements by class name |

### Changing HTML Elements

| Property | Description |
| :--- | :--- |
| _element_.innerHTML =  _new html content_ | Change the inner HTML of an element |
| _element_._attribute = new value_ | Change the attribute value of an HTML element |
| _element_.style._property = new style_ | Change the style of an HTML element |
| Method | Description |
| _element_.setAttribute_\(attribute, value\)_ | Change the attribute value of an HTML element |

### Adding and Deleting Elements

| Method | Description |
| :--- | :--- |
| document.createElement\(_element_\) | Create an HTML element |
| document.removeChild\(_element_\) | Remove an HTML element |
| document.appendChild\(_element_\) | Add an HTML element |
| document.replaceChild\(_new, old_\) | Replace an HTML element |
| document.write\(_text_\) | Write into the HTML output stream |

### Adding Events Handlers

| Method | Description |
| :--- | :--- |
| document.getElementById\(_id_\).onclick = function\(\){_code_} | Adding event handler code to an onclick event |



