# ASCII-ART Method of CSS Grid

Whenever we build simple or complex layouts using Grid. Mostly, We position the items against line numbers. Because by default, Grid Layouts landed with Grid lines holding positive and negative line numbers. Positioning items against line numbers is a fine way. Though grid has numerous ways to accomplish the same with an undersized cognitive encumbrance. Likewise, ASCII-Art Method has added unique features from the crowd.

## Table of content

    - Describing ASCII-Art Layout
    - Protocols for applying ASCII-Art Method
    - ASCII-Art Placement is better than  Line Based Placement
    - An Universal Use case
    - Line Names allocated implicitly
    - A minimal Use case
    - Accomplish the Modern Layouts
    - Wrapping up

## Describing ASCII-Art Layout

When we declare an element as a grid container using `display: grid`. By default, the Grid container landed with a single column track and sufficient rows are generated. If child items participate in the grid which converted to grid items irrespective of their `display` property.

For Instance, Create an explicit grid by defining columns and rows using `grid-template-column` and `grid-template-rows`. Here, We Create two columns that share the free space equally and three rows with a track size of 200px.

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 200px 200px 200px;
}
```

Illustrate the defined explicit grid by dev tools as below,

![Rows and columns](/assets/Explicit-Grid.jpg)

Currently, We have handed with two column tracks and three row tracks. So, Just Start to define our layout in ASCII-Art Style. We can define the entire layout within the grid container using named grid areas.

In the above explicit grid, We have two cells for each row and assign a name for each cell using the `grid-template-areas` property. According to the spec, Initial value of `grid-template-areas` is `none`.

```css
grid-template-areas = none | <string>+
```

`<string>+` is listing the group of strings enclosed with a quote. Each string is represented as a cell. Each quoted string is represented as a row.

For Instance,

```css
grid-template-areas:
  "head head"
  "nav  main"
  "foot foot";
```

The value of `grid-template-areas` describes the layout as having four grid areas. They are,

- head
- nav
- main
- foot

`head` and `foot` span two column tracks and one row track. Remaining `nav` and `main` span one column track and one row track. The value of `grid-template-areas` seems ASCII-Art style and At the same time, We can get a visualization of the overall structure of the layout from the CSS itself which is the most trouble-free way to understand it.

To understand how the value of `grid-template-areas` gets plotted in a grid, observe the below illustration.

![named template areas](/assets/value-of-grid-template-areas.gif)

Using `grid-template-areas`, We created our layout having four grid areas(head, nav, main, foot).

Now, Start to position the grid items against named grid areas instead of line numbers. Accordingly, Place a `header` element into the named grid area `head`, Specify the named grid area `head` in the `header` element using `grid-area` property.

> Named grid area in the grid layout also called as **ident**

```css
header {
  grid-area: head;
}
```

Likewise, Place the `nav`, `main`, and `footer` in named grid areas `nav`, `main`, and `foot` using `grid-area` property.

```css
nav {
  grid-area: nav;
}
main {
  grid-area: main;
}
footer {
  grid-area: foot;
}
```

## Protocols for applying ASCII-Art Method

According to the CSS Grid Layout Module Level 1, All strings must be defined under the following tokens,

- Named cell token
- Null cell token
- Trash token

### Named cell token

Represent the named grid area in the grid. For instance, `head` is a named cell token

### Null cell token

Represent the unnamed grid area in the grid container. For instance, **empty cell** in the grid is a null cell token.

### Trash token

A Syntax Error, An invalid declaration. For instance, Having a disparate number of cells in rows makes the definition invalid.

In `grid-template-area` definition,

- Every quoted string (rows) must have the same number of cells and Define the complete grid without ignoring any cell.

![Do's and Dont's of ASCII-Art Definition](/assets/Do's-and-Dont's.jpg)

- Need to ignore a cell or leave it as **empty cell**, Use full stop character(`.`)
  For instance from CSS Grid Layout Module Level 1,
  ```css
  #grid {
    display: grid;
    grid-template-areas:
      "head head"
      "nav  main"
      "foot .";
  }
  ```
  If you feel need more organized as well as more ASCII-Art styled definition for empty cells, use needed full stop characters without space between them.
  For instance from CSS Grid Layout Module Level 1,
  ```css
  #grid {
    display: grid;
    grid-template-areas:
      "head head"
      "nav  main"
      "foot ....";
  }
  ```
- A named cell token can span multiple grid cells, But those cells must form a rectangular shape. Currently, we can't create 'L' or 'T' shaped areas.

> According to the CSS Spec, Non-rectangular or disconnected regions may be permitted in a future version of this module.

## ASCII-Art Placement is better than Line-Based Placement

In line-based placement, Every grid item is placed against line numbers. Accordingly, Some grid item's line numbers get disparate for each breakpoint. Every time, We can't look back on line numbers used. At the same time, it takes cognitive encumbrance to understand the code after some time.

In ASCII-Art placement, Redefine the layout for each breakpoint using `grid-template-areas` within the grid container, and convenient to see how the layout will look from the CSS.

Using dev tools, we can enable to display the line numbers as well as grid areas. In firefox dev tools, Go to the `layout` panel. under `grid` tab, You can find the `grid display settings` and enable the `display line number` and `display area names`. These steps are similar to other dev tools also.

![Enabling grid settings](/assets/Grid-Display-Settings.jpg)

Compare to line-based placement, ASCII-Art placement furnished the named grid areas as well as line numbers which require less effort to visualize and easily find the placement of elements.

In the below illustration, Require to position a `header` element on the first row track and span two column tracks. From comparing the below two disparate placements, Finding the line numbers take more cognitive encumbrance than finding the Named grid areas.

![Line-based placement vs ASCII Art placement](/assets/line-based-vs-ASCII-Art.jpg)

## An Universal Use case

ASCII-Art is commonly named as named template areas. Whenever we try to explore the named template areas. There is a universal use case explained in every resource. This use case has the pattern of `header`, `footer`, `sidebars`, `main`.

![An Universal Use case](/assets/Universal-Usecase.png)

Implementing this use case in ASCII-Art style seems straightforward way and more understandable. Assign the ident to each element using `grid-area` only once in Base styles and No need to repeat it at every breakpoint. Redefine the layout for each breakpoint using `grid-template-areas` and Sometimes, Require to update the track listing using `grid-template-columns` and `grid-template-rows`. These guidelines will be similar to all kinds of layouts. Let's dig to build the layout from smaller breakpoints will be a well-behaved approach. Commonly called as **Mobile-First approach**.

For Mobile Breakpoint, Everything will be stacked. Before defining the layout, Assign an ident to each element using `grid-area` property as the base style.

```css
header {
  grid-area: head;
}

.left-side {
  grid-area: left;
}

main {
  grid-area: main;
}

.right-side {
  grid-area: right;
}

footer {
  grid-area: foot;
}
```

Now, Define the layout for Mobile Breakpoint.

```css
.parent {
  display: grid;
  grid-template-areas:
    "head"
    "left"
    "main"
    "right"
    "foot";
}
```

The layout gets rendered as below,

![Mobile breakpoint](/assets/Mobile-breakpoint.jpg)

By default, Every grid item will be **auto-sized** which seems a little bit weird. So, we set the `min-height` of `100vh`. Every grid item getting an equal breathing room makes the fine layout.

```css
.parent {
  display: grid;
  grid-template-areas:
    "head"
    "left"
    "main"
    "right"
    "foot";
  min-height: 100vh;
}
```

![Mobile breakpoint with min-height](/assets/Mobile-breakpoint-with-equal-space.jpg)

For Tablet breakpoint, Main gets landed beside the sidebars. The Left and right sidebars get stacked. consequently, Require to update the track listing as two columns and four rows explicitly.

Accordingly, we redefine the layout as below,

```css
.parent {
  grid-template-columns: 0.5fr 1fr;
  grid-template-rows: 100px 1fr 1fr 100px;
  grid-template-areas:
    "head head"
    "left main"
    "right main"
    "foot foot";
}
```

![Tablet breakpoint](/assets/Tablet-breakpoint.jpg)

For Desktop breakpoint, A few tweaks in tablet breakpoint. sidebars get desperate into individual columns. Accordingly, Update the track listing as three columns and redefine the layout as below,

```css
.parent {
  grid-template-columns: 200px 1fr 200px;
  grid-template-areas:
    "head head head"
    "left main right"
    "left main right"
    "foot foot foot";
}
```

![Desktop breakpoint](/assets/Universal-Usecase.png)

Take a look at the below codepen, An universal use case implemented alike explained above, and see how this layout gets changed for each breakpoint:

{% codepen src="https://codepen.io/preethi-dev/pen/bGvmbZK" %}

## Line Names allocated implicitly

According to CSS grid layout module level 1, `grid-template-areas` generate **implicity named grid lines** from named grid areas by default. Each named grid area has four implicity named grid line: `-start` append to name of the grid area for starting lines of each grid area and ending lines of each grid area have `-end` append to name of the grid area

Each implicitly named grid line behaves as same as any other named grid lines. They do not appear in `grid-template-columns` and `grid-template-rows`. If we specify explicitly named grid lines, Then the track line will have both explicitly and implicitly named grid lines. Both work the same.

For instance,

For named grid area `head`, Four implicitly named grid lines are created. Row-start and column-start lines are named `head-start`. Alike, Row-end and column-end lines are named `head-end`. Two `head-start` and two `head-end` are implicitly named grid lines of the named grid area `head`.

![Implicitly assigned line names](/assets/Implicitly-assigned-line-names.jpg)

In view of the fact that anyone of the cell can't share disparated named grid areas. Consequently, We can't achieve the overlay technique in ASCII Art layout. Though this can be accomplished by implicitly assigned line names. We can place a grid item as an overlay using implicitly assigned line names.

Use the same `grid-area` property, For assigning the implicitly assigned line names to `overlay` element. Line-based placement as well used the `grid-area` as a shorthand property to place grid items against line numbers. Order of `grid-area` property's value is opposite to box-sizing property's value such as margin, padding.

The order of `grid-area` property's value is

```css
grid-area: block-start / inline-start / block-end / inline-end;
```

According to the Logical properties and value level 1, `block-start`, `block-end`, `inline-start`, and `inline-end` are flow relative values relates to the flow of content. Accordingly, They can change if the text direction or writing mode gets changed. whereas, The term `block` indicates the content flow from top to bottom direction. For instance, Paragraphs are laid out one below the other. The term `inline` indicates the left to right direction. For instance, Words in a sentence are laid out from left to right if it's LTR language.

![Block and inline flow](/assets/Block-and-inline-flow.jpg)

In Simple words, the Row axis referred to the block axis. The column axis referred to an inline axis.
The block axis properties are `grid-row-start` (block-start) and `grid-row-end` (block-end). The inline axis properties are `grid-column-start` (inline-start) and `grid-column-end` (inline-end). Based on that, `grid-area` shorthand properties works.

```css
grid-area: grid-row-start / grid-column-start / grid-row-end / grid-column-end;
```

![Block and inline axis](/assets/Flow-relative-direction.jpg)

This `grid-area` property will be helpful to position the element against the line number or named grid lines or an ident (named grid area). For instance, Let's take the universal use case having the pattern of `header`, `footer`, `sidebars`, `main`. Create an overlay that occupies `sidebars` and `main`. Using `grid-area` property, Position the overlay against implicitly assigned line names using the below CSS,

```css
.overlay {
  grid-area: left-start / left-start / right-end / main-end;
}
```

Take a look at the below codepen, An overlay implemented in a universal use case like explained above, and see how this overlay is positioned across all breakpoints:

{% codepen https://codepen.io/preethi-dev/pen/gOeBWWL %}

## A minimal Use case

Occasionally, Require to implement the grid in part of the container. Alike a container having `main` and `footer`, Require to apply the grid in `main` alone as below,

![Minimal Layout](/assets/Minimal-Layout.jpg)

In `main`, Require to position the `.image` and `.text` div blocks by ASCII-Art style. For Mobile breakpoint, Define the track list as a 4-column grid and the layout will be `.image` and `.text` span four column tracks and one row track as follow:

```css
main {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas:
    "image image image image"
    "text  text  text  text";
}
```

Assign the idents to corresponding div blocks using the below CSS:

```css
main .image {
  grid-area: image;
}

main .text {
  grid-area: text;
}
```

Using dev tools, We can clearly visualize the named grid areas like below,

![For mobile breakpoint](/assets/Minimal-Mobile-Breakpoint.jpg)

For Small Tablet breakpoint, Redefine the layout using named cell token and null cell token for leaving an empty cell and require to redefine the track list as a 6-column grid using the below CSS:

```css
main {
  grid-template-columns: repeat(6, 1fr);
  grid-template-areas:
    "image image image image image image"
    "..... text  text  text  text  .....";
}
```

Dev tool visualization:

![For Small Tablet breakpoint](/assets/Minimal-Small-Tablet-Breakpoint.jpg)

For Large Tablet breakpoint, Redefine the layout and update the track listing as an 8-column grid using the below CSS:

```css
main {
  grid-template-columns: repeat(8, 1fr);
  grid-template-areas:
    "image image image image image image image image"
    "..... text  text  text  text  text  text  .....";
}
```

Dev tool visualization:

![For large tablet breakpoint](/assets/Minimal-Large-Tablet-Breakpoint.jpg)

Finally for larger breakpoints like laptop and desktop, Redefine the layout and update the track listing as a 12-column grid using the below CSS:

```css
main {
  grid-template-columns: repeat(12, 1fr);
  grid-template-areas:
    "image image image image image image image image image image image image"
    "..... text  text  text  text  text  text  text  text  text  text  .....";
}
```

Dev tool visualization:

![For Laptop and Desktop breakpoint](/assets/Minimal-Laptop-Desktop-Breakpoint.jpg)

See the below code pen how the layout adapts to every breakpoint:

{% codepen https://codepen.io/preethi-dev/pen/rNdqBbX %}

## Accomplish the Modern Layout

Previously, We look at a minimal and simple layout using `grid-template-areas`. Now, Moving on to the modern layout which little bit tricker. But, We can accomplish it smartly by ASCII-Art style. Let's attain the below layout slowly but surely.

![Modern layout](/assets/Modern-Layout.jpg)

Apart from the base styles, Start digging into a crucial part. Let's define the layout and assign the idents to corresponding elements. In this layout, Apply the grid on `main` alone and `header` accomplished by flexbox. In `main`, Required to position the three `.image` blocks and a single `.text` block against named grid areas.

For Mobile breakpoints, Define the layout and track listing using the below CSS:

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas:
    "image1 image1 .....  image2"
    "texts  texts  texts  texts"
    ".....  image3 image3 .....";
}
```

Assign the idents to corresponding div blocks as below,

```css
.image:nth-child(1) {
  grid-area: image1;
}

.image:nth-last-child(2) {
  grid-area: image2;
}

.image:nth-last-child(1) {
  grid-area: image3;
}

h2 {
  grid-area: texts;
}
```

Dev tool visualization:

![For mobile breakpoint](/assets/Modern-Mobile-Breakpoint.jpg)

Now, You can visualize the above defined layout effortlessly without any explanation. That's the spotlight of ASCII-Art layout.

For tablet breakpoints, Redefine the layout and track listing using the below CSS,

```css
.grid {
  grid-template-columns: repeat(8, 1fr);
  grid-template-areas:
    ". image1 image1 .      .       .      image2 ."
    ". texts  texts  texts  texts   texts  image2 ."
    ". .      image3 image3 image3  image3 .      .";
}
```

Dev tool visualization:

![For tablet breakpoint](/assets/Modern-Tablet-Breakpoint.jpg)

For laptop and desktop breakpoints, Redefine the layout and update the track listing as a 12-column grid using the below CSS,

```css
.grid {
  grid-template-columns: repeat(12, 1fr);
  grid-template-areas:
    ". image1 image1 .      .       .      .      .      .      .      .      ."
    ". texts  texts  texts  texts   texts  texts  texts  texts  texts  image2 ."
    ". .      image3 image3 image3  image3 .      .      .      .      .      .";
}
```

Using the negative `margin` hack, First image overlapped on heading.

Dev tool visualization:

![For laptop and desktop breakpoint](/assets/Modern-Desktop-Breakpoint.jpg)

See the below code pen how the layout adapts to every breakpoint:

{% codepen https://codepen.io/preethi-dev/pen/gOeBYNo %}

## Wrapping up

- In ASCII-Art layout, Define the layout using `grid-template-areas` and assign the idents using `grid-area`.

- While defining the layout, Use named cell tokens and null cell tokens.

- As well as make sure with each row has the same number of cells. Ignoring a single cell doesn't create a layout means considered a trash token.

- For better visual, Use required whitespace between the string while defining the layout. Make sure with no whitespace inside the null cell token(eg: .....) Otherwise, A single whitespace found between null cell tokens Then creates unnecessary empty cells which make the layout invalid.

- Require to reposition the grid items for each breakpoint then redefine the layout within the grid container and update the track listing if needed. No need to touch the grid items.

- By default, Named grid areas have four implicitly assigned line names. Two for row tracks and another two for column tracks.
