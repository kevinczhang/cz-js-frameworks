---
description: Node.js is perfect for event-driven applications.
---

# Event

Every action on a computer is an event. Like when a connection is made or a file is opened.

## Events Module

Node.js has a built-in module, called "Events", where you can create-, fire-, and listen for- your own events. To include the built-in Events module use the `require()` method. In addition, all event properties and methods are an instance of an EventEmitter object.

```javascript
var events = require('events');
var eventEmitter = new events.EventEmitter();

//Create an event handler:
var myEventHandler = function () {
  console.log('I hear a scream!');
}

//Assign the event handler to an event:
eventEmitter.on('scream', myEventHandler);

//Fire the 'scream' event:
eventEmitter.emit('scream');
```
