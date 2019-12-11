## INTRODUCTION
### WHAT IS BOOTSTRAP? 
 It is a CSS framework that provides us with a simplified version of css properties. The main interesting thing about Bootstrap is that you can declare classes inside the html class property that represent those css properties that would be otherwise too time consuming to write in its own css file.

### WHAT DOES BOOTSTRAP DEPEND ON? 
 In order to function properly, Bootstrap depends on Javascript and Popper.js

## GETTING TECHNICAL

### ORDER OF DECLARATION MATTERS INSIDE A .HTML FILE 
 On the first step, the CDN $(CONTENT DELIVERY NETWORK) link to Bootstrap should be declared inside the <header> tag. Then, the following <scripts> should be declared before the closing </body> tag, maintaing the following order:
1. `JQuery`
2. `Popper.js`
3. `Bootstrap.js`

### VIEWPORT META TAG 
 Declared inside \<header>, allows responsive behavior.

## BOOTSTRAP SPECIFICS

###  CONTAINERS 
* basic layout element
* required when using bootstrap's grid system
* required for bootstrap's grid system

> `.container`
> * Custom width.
>
> `.container-fluid`
> * Occupies full width of a page.
> * Spans the entire width of the viewport.

### OUTER MEDIA QUERIES 
 Breakpoints that allow you to modify your site according to the size of the screen $(VIEWPORT) or according to the type of device that's accessing your site.

## GRID
### COLUMNS AND CONTAINERS
* Containers make grids responsive. 
* Grids consists of rows and columns.
* Columns `.col` are contained in rows `.row`.
* Columns are separated by a gutter. 
* Columns without a specified width automatically layout as equal width columns.
* Columns width are set in percentages, so they're always sized relative to their parent element.
* Variety:  `.col-4 ` `.col-sm`
* Syntax: `.col-<breakpoint>-<fraction of space>` 
```mermaid
graph LR
    A[w-100]-->B;
    B[width: 100% !important]-->A;
```


### FRACTIONS OF SPACE AND BREAKPOINTS
* Available breakpoints: `sm`  `md`  `lg` `xl` .
* A grid is divided in 12 equal horizontal parts.
>`.col-xl` activates for large screens and up.
`.col-sm` activates for small screens and up.
`.col-sm-6` this column will occupy 6/12 (half the size of the grid) and will activate for small screens and up. 
`col-md-auto` this column will size based on the natural width of its content and will activate for medium screens and up.

### COLUMN GUTTER
> Gutters can be imagined as black lines that separate columns from each other. A gutter, simply put, is the padding between two columns
> * `.no-gutter` removes gutters


## DISPLAY PROPERTY
* `.-d-{breakpoint}-{property}`
> `.d-md-none` sets display to none for medium screens and up.
> `.d-print-flex` sets display to flex when printing the html page.

## FLEX PROPERTIES
* `.flex-{breakpoint}-{flex-direction}` 
* `{.justify-content|align-content}-{breakpoint}-{start|end|center|between|around}` 
* `{.align-items|.align-self}-{breakpoint}-{start|end|center|baseline|stretch}` 
* `.flex-{breakpoint}-{grow|fill}-*`
* `.flex-{breakpoint}-{wrap|nowrap|wrap-reverse}`
* `.order-{breakpoint}-*`
**PS**: search for -> auto margins on bootstrap
### FLEX FILL
* `.flex-{breakpoint}-fill` forces the element into a width equal to the size of its content

## SPACING PROPERTIES
*`.{property}{sides}-{breakpoint}-{size}`

### PROPERTY
* `m` - margin
* `p` - padding

### SIDES
* `t | b | l | r` top, bottom, left, right
* `x | y` left, right | top, bottom

### SIZE
* 1-5 | auto | negative margin (n1-n5)
## VISIBILITY
* `.{invisible|visible}`
## OVERFLOW
*.`.overflow-{hidden|auto}`
## BORDER
*`border-{[]|top..}-*`
*`.rounded-{sm|lg}` size of border-radius
*`.rounded-{circle|pill}`

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3NjMzMTg1OSwtMzYxMTg3NzEzXX0=
-->