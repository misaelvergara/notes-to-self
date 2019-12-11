## Single-page application (SPA)
A single-page application is built in a single html file. The dynamic changes to this page are handled Javascript on the client-side of the application, therefore, on the user's browser.

The page is built up with components and every component is a React component. The entire page is managed by a root component. 

```javascript
ReactDOM.render(); 
// typically single call by the root application
```

## Multi-page application (MPA)
A multi-page application is built under multiple html files, each container their own content. In this scenario, React is used to render widgets.
```javascript
ReactDOM.render(); 
// proportional calls to the n# of widgets 
```

> **ES6** : NEXT GEN JAVSCRIPT FEATURES
> **State** is the data that the application depends on.
> **Build Workflow**: are the standards we follow to develop an application.
> **Bundles**: piles your code into a single file, avoiding separate files that would require your application to run multiple requests, consuming unnecessary resources. We use **Webpack** to bundle our project.
> **Development Server**: a server that runs on a local machine
> **Dependency Management**: npm
> **Stateful Components**: is a component that manages state
> **Side-effects**:


## CSS Pre-Fixes and Linting
> Auto

## `{ <property> }`
> Dynamic outputter
## `props.children`
> Children is a reserved keyword that outputs elements that a component wraps.
``` javascript
App = () = {
	return (<Component> <children> </Component>);
}
```
## Radium
> Allows the usage of pseudo-selectors and media-queries inside a .jsx file.


## `useState();`

``` javascript
const [currentState, setState] = useState(<initial state>);
```
> The useState method returns an array that contains two elements. The first elements refers to the state value that was passed to the method as a parameter. The second element refers to a function that updates the value of that particular state. 

> Unlike the state properties that is used inside classes, the useState hook does not merge the values of a state upon setting a new state. The setState function updates the state entirely, replacing the old state with the new state.

## Arrow Functions and Bind method
``` javascript
class App extends Component {
	state = {
		value: 0
	}
	newValue = (i) => {
		setState({ value: i });
	}
	
	return(
		<div onClick={ () => newValue(1) } value={value} />
		<div onClick={ newValue.bind(this, 1) } value={value} />
	);
}
```

## Two-way Data Binding
``` javascript
class App extends Component {
	state = {
		name: 'Joshua'
	};
	
	nameChangedHandler = event => {
		setState({ event.target.value });
	}
	
	return(
		<div>
			{ this.state.name }
		<div/>
		<input onChange={ nameChangedHandler }/>
	);
}
```
> Event is a default object to React.

## Functional Components
> Receives `props` as a parameter. Should be used in the majority of cases unless access to Lifecycle hooks or state management is necessary. 


## Rule Of Thumb
The component that owns a piece of the state should be the one modifying it.

##
When there is no parent-child relationship between two components and you want to keep them in-sync, sharing data between them, you need to lift the state up and pass it via props.


## Event Handlers
The Event Handler is the function that handles a said event. E.g: 
```javascript
	handleClick() {
		console.log("WHO dared to click me!?!!");
	} // this function IS the event handler		
	// click is the event being handled
```
The event "bubbles up" all the way up to its ancestors, calling their handlers for that specific event.

## Lifecycle Hooks
Only available in class components.
components go through a few phases during their life cycles
1. mounting phase
> when the instance of a component is created and inserted into the dom
> > components are rendered recursively. which means, parents get rendered and then their children=-- 
> some methods are called during this phase, these methods are called lifecycle hooks
> 1. constructor
> 2. render
> 2. componentDidMount 
2.  update phase
>  happens when the state or the props of a component gets changed
>  1. render
>  2. component did update
3. unmount
> 1. componentWillUnmount