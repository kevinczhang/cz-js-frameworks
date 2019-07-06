# String

### char can be accessed using charAt

```javascript
var str = "HELLO WORLD";
str.charAt(0);            // returns H
str.charCodeAt(0);         // returns 72
	
var letterX = letters.indexOf("m"); // This is at index 0.
word.length // 5
```

### replace \(original string won't be modified\)

```javascript
// Replace first instance of bird with frog.
var result = animals.replace("bird", "frog");

// Replace all matching patterns with a string.
// ... Remove the g to only replace the first match.
var result = data.replace(/ca\w/g, "test");
```

### Split String to Array

```javascript
var colors = "blue+orange+red+yellow";
var result = colors.split("+"); // split on plus sign
var results = data.split(/\W+/); // split on one or more non-word
var arr = str.split("");   // Split in characters
```

### substring

```text
var value = "cat123";
	// ... Start at index 0.... Continue until index 3.
var result = value.substring(1, 3); // at
	• slice(start, end) // can use negative
	• substring(start, end) // can't use negative
	• substr(start, length)
```

### Equals

```javascript
== allow type conversion so "800" equals 800
=== not allow type conversion so "800" not equals 800 
!== not allow type conversion either
	
=== and !== is recommended
```

### Common methods

```text
toUpperCase();
toLowerCase();
```

