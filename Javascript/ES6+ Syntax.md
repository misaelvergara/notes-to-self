
# Faz o que? Por qual meio? Por quê?
Functions
---
**`function name() {}`** is a function declaration. Therefore it is affected by **hoisting**, which means the function `name()` is available for execution even before it is declared. Whereas function expressions, such as **`const expr = () => {}`**,  are not.
```javascript
greet() // says hi
expr() // undefined
function greet() { /* says hi */ }
const name = () => { /* says name */ }
```
Operators
-------------
_**`Rest Parameter`**_ | **`...`** makes it possible to declare variadict functions **[? one that takes a varying number of arguments]**. It "spreads out" the remaining arguments.
```javascript
funciton sum(el1, el2, ...args) {
	return el1 - args[0] - el2 + args[1];
}
sum(1,7,8,8); // ---> 6
```
---
_**`Spread Operator`**_ | **`...`**  allows the spreading of elements of an iterable collection (like an array or even a string) into both literal elements and individual function parameters.
```javascript
let string = "bane";
let stringArray = ...string; // ---> ['b', 'a', 'n', 'e']
```
Objects
----------
_**`Property Shorthand`**_ Object properties that have the same name as outer scope variables must simply be declared instead of being assigned explicitly to their _**correlated**_ [_**?**_ have a mutual relationship or connection, in which one thing affects or depends on another ] values.
> [_?_ Shorthand | a technique, a method of rapid writing by means of abbreviations and symbols]
```javascript
// -> outer scope
let x = 0, y = 20;
const obj = {x, y /* -> inner scope */};
// - - - - -
const olderSyntaxObject = {x: x, y: y}
```

___
_**`Destructuring`**_ pulls out properties of an array or object into single variables
```javascript
const array = ["June", "St. 172"];
const [name, address] = array; // array destructuring

const object = { name: "Rhuanna", address: "Av. 1212"};
const {name: name_2, address: address_2, phone_2 = 33001138} = object;
/* 
* @phone_2 is a default value for the object being deconstructed
* that means that if a "phone_2" property was declared, its value
* would take priority over the default "phone_2 = 3300.." value
*/

// deep match destructuring
const obj = { title: 'phrasal verb', nested: {prop: 'value'}};
const { title, nested: { prop: value }} = obj;
// ---> const title, const value
```
___
_**`Computed Properties`**_ are properties that can be expressed in the form of a expression
```javascript
const nameTeller = () => "Joanne";
const obj = {
	[nameTeller() + "vv"]: "value",
}

console.log(obj[nameTeller()+"vv"]); // same as obj.Joannevv
```

Classes
---------
**`get`** | **`set`** are shorthands for getters and setters
```javascript
class Shape {
	constructor(height) {
		this._height = height;
	}
	set height(height){ 
		this._height = height;
	}
	get height(){ 
		return this._height;
	}
}

new Shape().height = 1221; // sets 1221
new Shape(1222).height; // returns 1222
```
___
_**`Iterators`**_ go by each value of a collection, returning their assigned value. Arrays and strings are natively iterable by `for-of` loops. However, objects are not natively iterable. If you intend to make an object iterable by a `for-of` loop, a method called `Symbols.iterator` must be implemented as a property. 
> An iterator is a pointer for **traversing** [**_?_** to travel across or through something | passando pelo meio ou através de algo ] the elements of a data structure.
> 
> _**`Data Structure`**_ is a collection of data (? tiny pieces of information). The Data Structure contains them, the relationships among them and the functions that can be applied to them.
> _**`Structure`**_ is an arrangement of something complex and the ways of which the things that form this complex thing are related.
> 
```javascript
const object = {
	name_0: 'value',
	name_1: 'value I',
	name_3: 'value II',
	// returns an object containing the next() method
	[Symbol.iterator]() {
		let step = 0;
		const values = Object.values(object);
		return {
			// returns an object containing the value and done properties
			next() {
				if (values.length <= step) {
					return { value: undefined, done: true }
				}
				return { value: values[step++], done: false }
			}
		}
	}
};
```
> *`Reference`* : https://codeburst.io/a-simple-guide-to-es6-iterators-in-javascript-with-examples-189d052c3d8e
___
_**`Generators`**_ are functions that can stop mid-way the *control flow* and then continue from where it stopped. Generators return an object that contains the `next()` method which in turn returns an object containing the `value` and `done` properties.
- _**`return`**_ | _**`yield`**_ using the `return` statement before an `yield` statement will prevent results from being yielded, for it also assigns true to the `done` property.
```javascript
function* generator() {
	console.log('hi');
	yield 1;
	// return;
	console.log('bye');
	yield 0;
}

let _yield = generator().next().value; // 2

for (let val of generator()) {  
	console.log(val);  
}
```
> *`Reference`* : https://codeburst.io/understanding-generators-in-es6-javascript-with-examples-6728834016d5
> *`Reference`* : https://exploringjs.com/es6/ch_generators.html#sec_generators-as-observers
> 
