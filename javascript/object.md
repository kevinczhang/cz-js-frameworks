# Object

#### Initialization

```javascript
var box = {
    width: 2,
    height: 3,
    area: function() {
	return this.width * this.height;
    }
};

// Write object properties.
document.write(box.width + "; " + box.height + "; " + box.area());
```

#### Properties and functions can be accessed with . or index \[\]. If not there then return undefine

```javascript
var lookup = {"cat": 400, "dog": 600};
document.write(lookup.cat + "; " + lookup["cat"] + "; ");
```

#### Loop over keys

```javascript
var result = Object.keys(test); // Get keys.
	// ... Write the keys in a loop.
for (var i = 0; i < result.length; i++) {
    document.write(result[i] + "; ");
}
```

#### It can be used as dictionary as in C\# or map as in Java, when the key is not integer

