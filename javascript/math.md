# Math

### Constants

```javascript
Math.PI
Math.round()
Math.round(4.7);    // returns 5
Math.round(4.4);    // returns 4
Math.pow(8,2);      // returns 64
Math.sqrt(64);      // returns 8
Math.abs(-4.7);     // returns 4.7
Math.ceil(4.4);     // returns 5
Math.floor(4.7);    // returns 4
Math.sin(90 * Math.PI / 180);     // returns 1 
Math.cos(0 * Math.PI / 180);     // returns 1 
Math.min(0, 150, 30, 20, -8, -200);  // returns -200
Math.max(0, 150, 30, 20, -8, -200);  // returns 150
```

### Random

```javascript
Math.random();     // returns a random number
Math.floor(Math.random() * 10);     // returns a number between 0 and 9
Math.floor(Math.random() * 10) + 1;  // returns a number between 1 and 10
```

This JavaScript function always returns a random number between min \(included\) and max \(excluded\):

```javascript
function getRndInteger(min, max) {
    return Math.floor(Math.random() * (max - min) ) + min;
}
```

This JavaScript function always returns a random number between min and max \(both included\):

```javascript
function getRndInteger(min, max) {
    return Math.floor(Math.random()*(max - min + 1)) + min;
}
```

