React
---
Is a framework for building SPAs (single page applications).

Not all browsers support next gen JS features. This way, a build workflow that can ship code to these browsers is needed, in order for your application to be supported across the widest range possible.
___
A **`build workflow`** gathers tools that will be a part of your development environment, helping you code better and faster.

A **`bundler`** is a tool that gathers all the separate files that make up your project into one huge "package file" on which browsers can read.

A **`compiler`** is a tool that translates your code into machine language that a computer's processor can use.

**Folder Structure**
**`public folder`** - is the folder that gets served by the web server. Like a waiter serves dinner.

**`index.html`** - is the single html page that receives injections from other files in order to show different views dynamically. 
> ↳ This page is like a sick patient. Whenever it is sick and in need of a specific medicine, a nurse comes around and gives it an injection.

Coding with React
---

**`JSX syntax`** gets compiled down to React.createElement functions

**`{ ? }`** - **`Dynamic Content Output Syntax`** - Imagine you are in the 80s and you operate writing machines, writing documents all day and fixing up typos that come up once in a while. Whenever a typo needs to be fixed, the text that comes before the typo needs to be re-written into a new document so that the typo can be fixed. Then, the text that comes after it also needs to be rewritten. Ok. DCOS is a way of dynamically changing a part of your document. Whenever you need a part of your document changed, you can specify a variable in curly braces so that the value of this variable will be shown in the real document. And that may happen whenever the value of this variable changes.

A component is represented by a component tag that represents its name when it is imported. Component selectors start with an uppercase letter because all HTML elements are reserved with a lowercase letter.


**`props`** - Imagine that a component is waiting to receive certain data so as to operate over this data and display something. This data can be passed as an "html attribute", a prop.
> **`props.children`** is a reserved word.
```jsx
// Header.js
const header = props => { 
	render() {
		return (
			<div>
				<h1>props.name</h1>
				props.children
			</div>
		)
	}
}
// Index.js
// imports above ..
(
	<Header name="John">Is a software engineer.</Header>
)
```
**`state`** - is the data that an application currently possess the use of.

[?leaner, ?prone to something, ?code parser, ?css linting, ?build workflow]	
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjQ4MTQwODVdfQ==
-->