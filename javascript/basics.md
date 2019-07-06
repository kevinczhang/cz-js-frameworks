# Basics

### Hoisting

Hoisting is the default behavior of moving all the declarations at the top of the scope.

###  **Closure**

When a function returns the other function the returning function will hold its environment and this is known as closure.

###  **Polyfilling**

It is one of the methodologies that can be used as a sort of backward compatibility measurement.

###  **Transpiling**

A tool that transforms code with newer syntax into older code equivalents and this process is called “Transpiling”.

### var vs let

var is function scoped and let is block scoped.

### Data Types

In JavaScript there are 5 different data types that can contain values: 

* string
* number
* boolean
* object
* function

There are 3 types of objects: 

* Object
* Date
* Array

2 data types that cannot contain values:  null and undefined

```javascript
typeof "John"                 // Returns "string" 
// You cannot use typeof to determine if a JavaScript object is an array (or a date).

"John".constructor                 // Returns "function String()  { [native code] }"

function isDate(myDate) {
    return myDate.constructor.toString().indexOf("Date") > -1;
}
```



