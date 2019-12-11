Introduction
---
**`What are Sagas?`** - Sagas are implemented as generator functions that yield objects to the redux-saga middleware.

**`How do Sagas work?`** - When a promise is yielded to the middleware, the middleware waits (suspends the saga that pushed the object) until the promise completes. Once the promise is resolved, the middleware will resume the saga.
___
> **`WORKERS`** - are tasks that handle actions upon demand. 
> [functions that are invoked to handle dispatched actions]
> 

> **`WATCHERS`** - are observers that watch for dispatched actions.
> [functions that get notified whenever a new action is dispatched]
> 

> **`EFFECTS`** - Redux-Saga is a middleware. Middlewares sit in between Redux dispatched actions and determine whether an action should be reduced or not.
>  In order for Redux-Saga to fulfill its role as a middleware, it offers **Effects**, which are methods that can be implemented inside Sagas in order to instruct Redux-Saga on what it should do.


Testing
---
Generator functions conventionally return an object that contains the `next()`  method. When `next()` is invoked, it returns an object that contains the following structure: 
```js
{ 
	done: boolean,
	value: any,
}
```
> **`value`** property **:** contains the yielded expression
> **`done`** property **:** indicates if the generator has terminated going over its **queue of expressions**

```js
// saga.js
export const delay = (ms) => new Promise(res => {
	return setTimeout(res, ms);
});
  
function* notifyNewLog() {
	console.log('NEW: CONSOLE LOG REQUEST')
}
function* worker() {
	// yield delay(1000);
	yield call(delay, 1000);
	yield({type: 'CONSOLE_LOG'});
}

function* watcher() {
	yield takeEvery('NEW_LOG', worker);
}

export default function* rootSaga() {
	yield all([watcher(), notifyNewLog()]); 
	/* ↳ makes both generators run in 
	parallel to each other */
} 
```
Following this design pattern asserts that the `worker()` function will yield a copy of the `delay()`, which helps us distinguish whether the `worker` returned the expression we expected.


**⇒ [ `all()`,  `dododo` ]** 



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk0MDQwMzM4NywxNzQyMDc2ODEsLTk0Mj
g4NDQ2Niw2NDI3NzQ2MjQsLTEzMzc4MjQ2MjAsNDk4MjA4NDk0
LC0xNTM5OTA0MzkxLC0yMDg4NzQ2NjEyXX0=
-->