# Array

In JavaScript, array is object. arrays use numbered indexes. objects use named indexes.

```javascript
// Use the following method to judge if it is an array: 
Array.isArray(colors );
if (colors instanceof Array)
```

#### Initialization

```javascript
var colors = ["red", "blue", "green"];
var len = colors.length;
```

#### It can be a stack, queue or map with index to be integers.

```javascript
var removed = colors.pop(); // Remove last
var added = colors.push("purple"); // Add to last
	// or 
colors[colors.length] = "Lemon";
var removed = colors.shift(); // Remove first
var added = colors.unshift("purple"); // Add to first (much slower)
```

#### Find a element in array:

```javascript
//	If an element matches, its index is returned. 
//	If nothing is found, the special value -1 is returned.
var result7 = codes.indexOf(7);
```

#### Loop over the array

```javascript
// Way 1
for (var i = 0; i < letters.length; i++) {
    document.write(letters[i] + "; ");
}

// Way 2
letters.forEach(element => {
    document.write(element);
});

// Way 3
for (var i in array) {
    console.log(array[i]);
}

// Way 4  
for (s of myStringArray) {
  // ... do something with s ...
}
```

#### Slice \(remove only and will not change original array\)

#### Splice \(remove and add, this will change original\)

```javascript
<script>
	var codes = [10, 20, 30, 0, -1];
	var slice1 = codes.slice(1);
	var slice2 = codes.slice(1, 3);
	document.write(slice1 + "; " + slice2);
	
	codes.splice(1, 2, 900, 1000, 1100);
	document.write(codes);
</script>
	Output
	20,30,0,-1; 20,30
	10,900, 1000, 1100, 0, -1
```

#### Join Arrays

```javascript
var myChildren = myGirls.concat(myBoys);
```

#### Convert Array to string \(toString\(\) and join\(\)\)

```javascript
var words = ["note", "tip", "information"];
var result = words.toString();
	output: note,tip,information

var vehicles = ["car", "train", "plane", "boat"];
var result = vehicles.join("/");
	output: car/train/plane/boat
```

#### Sorting \(Both reverse and sort will modify original array\)

```javascript
colors.reverse();
patterns.sort(); // Sort naturally

<script>
	var numbers = [-1, 100, 10, 1, 2, 3]; 
	var compare = function(a, b) { return b - a; }; // Sort in reverse order 
	numbers.sort(compare);
	document.write(numbers + "; ");
</script>
	 Output  100,10,3,2,1,-1
```



