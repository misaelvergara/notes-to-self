What is Node.JS?
---
Node is a **runtime environment** for running JS. It is mainly used to build back-end services, also called APIs (application programming interface). Most modern applications are either connected to a server or to the cloud, to store data. Node excels at back-end services, being the fastest program available out there.

Node is essentially Google Chrome's V8 JS engine embedded in a C++ program. It also provides additional modules that give us capabilities not available inside browsers.

Node is **highly scalable** because of its non-blocking asynchronous architecture. A single thread is used to handle multiple requests. Like a single waiter handles multiples requests at a restaurant. When the chef is ready to serve the meal, it signals the **Event Queue**. Node is continuously monitoring this queue in the background. When it finds an event in this queue, it will take it out and process it. 

When a request is received on the server, a thread is allocated to handle that request. As a part of that request, it is probable that you'll want to query a database. This will take a while and meanwhile, another thread must be allocated to serve client requests. This synchronous architecure does not use resources suitably and, eventually, the server will run out of threads.
___
**`document`** | **`window`** objects are not defined in Node. For, these objects are a part of the runtime environment of browsers. Node has other special objects, such as `fs` [**_?_** file system], to work with files, the operating system and so on.
___
_**`Global Objects`**_ are objects that are part of the global scope and therefore can be accessed anywhere.
E.G: `window` is an object available for browser enabled JS engines. Any declaration is placed as a property of said object.
```javascript
let num = 2;
window.console.log(window.num); //equivalent to num
// the num file is scoped globally, which means it is
// accessible from anyfile
console.log();
```
____
Global Object and Modules Concept
---
The `global` object is the object that takes place of the `window` object in Node.JS. However, custom, declared variables/objects are only scoped to the file they are declared in. This happens because of Node's modular system, which **encapsulates** functions and variables declared in a file, making it unaccessible from anywhere else unless **required**. It's like they are declared private, from an OOP perspective.
```javascript
global.setTimeout(); // placed under the 'global' object
setTimeout(); // equivalent
```
___
Every node application has at least one file, which we call the **main module**. Every module has the `module` object which contains the `exports` property which serves as a mean to export variables and functions to other modules.
```javascript
// msg.js
const greet = (message) => { console.log(message) };	
const impact = (message) => {
	console.log(message.toUpperCase());
}
const nothing = () => {};
module.exports.greet = greet;
// exports greet() as a method of the greet object
exports.shout = impact; 
// exports impact() as a method of the shout object
// module.exports = nothing;
// overwrites the above exports and passes the nothing() function
// as the only exportable from msg.js

// the following syntax is not acceptable
// exports = nothing;
// because 'exports' is a reference to module.exports
// therefore, this is an attempt to overwrite the exports object
```
___
**`require`** function receives one argument that is the name of the target module. This function can be called inside modules to get access to the exportable variables and functions another module can serve. It takes up one param that can either refer to a relative path or a NPM module name. Therefore, your custom modules should begin with `./`.
```javascript
// main.js
const msg = require('./msg');
msg.shout.impact('hi') // --> HI
```
Behind the scenes, Node wraps your module in an IIFE [_**?**_ Immediately Invoked Function Expression] called the **Module Wrapper Function** as follows:
```javascript
(function(exports, require, module, __filename, __dirname){
// this is why you can call exports without preceeding the module object (module.exports) from a module
// your module is wrapped by this IIFE
})();
```
___
Node.JS Native Modules
---

_**`fs module`**_  have both asynchronous and synchronous methods. The latter always takes up a function of two params that either returns an error or the expected output.
```js
const fs = require('fs');

fs.readdir('./', error, success => {
	if (error) console.log(error);
	else console.log('These are the files and folders listed in'
	+ 'the current directory', success);
});
```
___
Events
---
Signal that something has happened.
___
**_`HTTP class`_** used to build a web server. Upon listening to a port, every time this port recieves a request, an event is **raised**. An **event listener** [_**?**_ a callback function that is called when an event is raised] responds to that event, reading the request and returning the right response. 

The `emit` method creates  **event raisers**. This method takes up two arguments: `eventName` and `eventArgs`.
```js
const EventEmitter = require('events');
const emitter = new EventEmitter();

emitter.on('messageLogged', event => {
	console.log('Listener called', event); // logs { message, type }
}); // event listener

emitter.emit('messageLogged', {message: 'test', type: 'anything'});
// raises an event
```
___
**Event Listeners** and **Event Emitters** cannot refer to the same event from different objects. 
> Bad Implementation
```js
// module_1.js
const EventEmitter = require('events');
const emitter = new EventEmitter();
function shout(msg) {
	console.log(`${msg} !!!`)
	emitter.emit('shout');
}
module.exports = shout;
// module_2.js
const EventEmitter = require('events');
const emitter = new EventEmitter();
const shout = require('./module_1');
emitter.on('shout', () => { console.log('shouted from somewhere') }; // THIS
// will not execute, 'shout' is being raised from a different instance of
// EventEmitter
shout('hi');
```
> Correct Implementation
```js
// module_1.js
const EventEmitter = require('events');
class Shouter extends EventEmitter {
	shout(msg) {
		console.log(`${msg} !!!`)
		// this class inherits ALL METHODS and ATTRIBUTES
		// from the EventEmitter class
		// emit is a method from the EventEmitter class
		this.emit('shout');
	}
}
module.exports = Shouter;
// module_2.js
const Shouter = require('./module_1');
const shouter = new Shouter();
shouter.on('shout', () => { 
	console.log('shouted from somewhere')
};
shouter.shout('hi');
```

**Event listeners** are created by calling the `on` method from an instance of `EventEmitter`. The most appropriate way of defining event raisers and emitters is by creating a class that extends `EventEmitter` and defining a method that calls `this.emit`. Why? Because if you create an object of `EventEmitter` inside two separate modules, on which one handles an event and the other listens to that event, the listener would not be able to listen to that specific event raised in a separate module, for it is a part of a different instance of EventEmitter, therefore, **an event is being raised from a different object, which results in divergence.**
____
_**`Event Arguments`**_ are the data that an event raiser sends to a listener upon being raised.
```js
const EventEmitter = require('events');
const emitter = new EventEmitter();

emitter.on('onRequest', eventArgs => {
	console.log(eventArgs.id)
}) // ---> 1

emitter.emit('onRequest', {id: 1, type: ''});
```
___



>> **jshint** -> gives descriptive detail about js errors `jshint msg.js`

[Implementation Detail, Public Interface]
Os botões do dvd e a parte com que o usuário interage é chamada de public interface. A placa mãe e o hardware interno do dvd é chamado de implementation detail. O usuário não precisa da última parte, somente   primeira para poder interagir com o DVD.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1NjY1ODI2OCwxNjQ3NTA3MzE2LDE0Mj
k0MDgyMjUsLTE1MTE4NzA3MSwtMTI1MDQzOTE3MywtNDg2NDg3
Nzk2LDEzODcxOTc4NjIsLTIwNjQwNTQ1MDMsLTE5MzI3Nzc3MD
gsMjAzNzc2OTI3NSwtMTc5MjYxMzgwNCwtMTA2MDcwNTkyMywt
MTY5NzEyOTA5MSwxNzY0Nzg4NDksLTE2MjE2MzU4NjcsLTEzOD
AzMzE0NDgsLTkzOTU5OTM4OSwtMjA2NDg2OTUyOSwtMTMwNzg3
MDIzMywxOTEwOTQ4MzA1XX0=
-->
