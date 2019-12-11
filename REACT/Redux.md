What is Redux?
--
Redux is a package that helps with state management in React and can be implemented as a message pattern that comunicates components between each other.


`Actions`  - set of instructions

**Type of Actions**
**`Event`** - dispatches an event, notifies of a change
**`Command`** - dispatches a command that invokes a procedure.
**`Document Action`** - saves data

**Routing Patterns for Actions**
**`Filtering`** - filter betwen multiple actions in order to accept a single defined action;
**`Mapping`** - takes an action and makes a decision based on the content of the action
**`Splitter`** - decouples a reducer from an action. Takes an action and splits it into multiple actions.

**Action Transform Patterns**
**`Enricher`** - Takes an action and enriches it with data that a component shouldn't be aware of.
**`Normalizer`** - Takes an action and normalizes its structure, passing it as another action.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1NzYyNjUyNywtMTg2OTM1MDM5MCwtNT
AxMzUxMjcxLC0xMjMwNjgyNDI4LC0xNDA3MzEyMTYzLC0xNTIx
MDM0Mzc1LDkzNzQxNzU5OCwtMTMyODI2Mjg3OSw3MjU0MDA3Mz
MsMTI4NDkwMzIzMl19
-->