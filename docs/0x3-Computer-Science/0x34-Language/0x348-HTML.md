# 0x348 HTML/CSS

## HTML

## CSS

### Basic
#### Selector
Note there is a non-trivial specificity ranking algorithm to resolve selector conflicts based on how specify each selector is.


**Basic Selector**

- universal selector
- element selector
- id selector
- class selector
- attribute selector

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
  
#### Box Model
Box sizing: the size of an element is specified with the `width` and `height` properties. Its interpretation depends on the `box-sizing` property
- `content-box` (default): width and height are width/height for the content area, so border, padding will add more width/height
- `border-box`: width and heights are width/height for the area inside borders (border + padding + content area)

##### Block and Inline
There are *block*, *inline*, *inline-block* elements, these can be set with the display property
```css
.hello {
    display: inline;
}
```

**Block element** 

- appears on its own line
- takes up the full width of its parent when no width is given
- height is just enough to fit its contents when no height is give

Examples are p, div, article...

**Inline element**

- appears inside the normal flow of text (according to the writing mode)
- only takes up enough width and height, setting width/height properties has no effect
- left-padding and right-padding works as expected but other padding and margin will not work normally (will affect other elements)

Examples are a, span, img, button, input...

**Inline-Block element**

- flow works like inline
- all padding, margin works as expected


## Reference
- [1] Attardi, Joe. "Modern CSS."

