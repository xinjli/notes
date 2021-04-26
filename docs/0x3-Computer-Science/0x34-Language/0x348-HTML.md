# 0x348 HTML/CSS

- [1. HTML](#1-html)
- [2. CSS](#2-css)
    - [2.1. Basic](#21-basic)
        - [2.1.1. Selector](#211-selector)
        - [2.1.2. Box Model](#212-box-model)
        - [2.1.3. Units](#213-units)
        - [2.1.4. CSS variables](#214-css-variables)
    - [2.2. Display](#22-display)
        - [2.2.1. Block and Inline](#221-block-and-inline)
        - [2.2.2. Flexbox](#222-flexbox)
        - [2.2.3. Grid](#223-grid)
- [3. Reference](#3-reference)

## 1. HTML

## 2. CSS

### 2.1. Basic
#### 2.1.1. Selector
Note there is a non-trivial specificity ranking algorithm to resolve selector conflicts based on how specify each selector is.


**Basic Selector**

- universal selector
- element selector
- id selector
- class selector
- attribute selector (e.g: [name]="value")

**pseudo classes** select elements based on some special states of the element

UI state

- :active: when activated, for button and links
- :checked: for radio button and select box
- :focus: for button, links and textbox
- :hover: triggered when mouse hover
  
Document Structure
- :first-child, :last-child: match the element that is the first or last of its parent


**pseudo elements** select only a part of the matched element

- ::first-line
- ::first-letter
- ::before, ::after: special pseudo elements which create first or last child of the matched element
  
#### 2.1.2. Box Model
Box sizing: the size of an element is specified with the `width` and `height` properties. Its interpretation depends on the `box-sizing` property

- `content-box` (default): width and height are width/height for the content area, so border, padding will add more width/height
- `border-box`: width and heights are width/height for the area inside borders (border + padding + content area)


#### 2.1.3. Units
Some common units are

- px: not recommended anymore, because css px is no longer 1-1 mapped to phyiscal pixels. only use this to setup default font-size
- em: relative unit, can cascade
- rem: root relative unit, will not cascade
- vw,vh: viewport width, height

#### 2.1.4. CSS variables

CSS variables is defined with `--varname` and referenced with `var(--varname)` function. They can be inherited by descendent elements

```css
:root {
    --heading-color: blue;
}
h1 {
    color: var(--heading-color);
}
```

### 2.2. Display

Commonly used display properties are `block`, `inline`, `flex` and `grid`.

#### 2.2.1. Block and Inline
There are *block*, *inline*, *inline-block* elements, these can be set with the display property

```css
.hello {
    display: inline;
}
```

**Block element** 

- appears on its own line
- takes up the full width of its parent when no width is given
- height is just enough to fit its contents when no height is given

Examples are p, div, article...

**Inline element**

- appears inside the normal flow of text (according to the writing mode)
- only takes up enough width and height, setting width/height properties has no effect
- left-padding and right-padding works as expected but other padding and margin will not work normally (will affect other elements)

Examples are a, span, img, button, input...

**Inline-Block element**

- flow works like inline
- all padding, margin works as expected


#### 2.2.2. Flexbox

A flexbox container is created by setting an element's `display` property to `flex`, this will create a block flexbox. To create an inline version, `inline-flex` is also available

`flex-direction` specify how to align the elements, it can be `row` (horizontal alignment) or `column` (vertical alignment)

#### 2.2.3. Grid


## 3. Reference
- [1] Attardi, Joe. "Modern CSS."

