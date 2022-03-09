# Notes from Duckett HTML and JS Books

HTML Book Chapters 3 and 13  
JS Book Chapters 2 and 4  

## HTML Book Chapter 3 Notes - Lists

Three types of lists are supported in HTML:  

- Ordered `<ol>`  
- Unordered `<ul>`  
- Definition `<dl>`  

Ordered and unordered list items are tagged with `<li>` elements.  
List Item tags can have a 'type' attribute added to change either:  

- Numbering type e.g. 1,2,3 vs a,b,c  
- Bullet style e.g. dots, arrows, etc  

CSS property `list-stype-type` can be used to change the numbering or bullet types.  

Definition Lists contain terms `<dt>` and definitions `<dd>`.  

- dt and dd have a 1+ to 1+ relationship.  
- There is not a one-to-one relationship requirement between dt and dd elements.  
- In effect, one term can have two definitions, or two terms can have the same definitions.  

Nesting Lists

- Create a new list inside of an existing one.  
- Browser will render the nested list indented from its parent.  
- Use CSS or element properties to adjust the icon/indicator for these sub lists.  

## HTML Book Chapter 13 Notes - Boxes

Topics Summary: Dimensions, Borders, Margins, Padding, and Show/Hiding of.  

### Dimensions  

Box Dimensions are:  

- Height  
- Width  

Measurements for sizing:  

- pixels: Absolute control of size.  
- percentages: Relative to browser window, or parent object e.g. another box.  
- 'em's: Bases size against the *font size* used within it.  

For flexibility, percentage and em are used.  

When content should be no smaller-than a certain width or height, use `min-width`.  
Conversely, use `max-width` to ensure the content/element does not get too large for the intended design.  
`min-width` and `max-width` can be used together to constrain content exansion or contraction.  
`min-height` and `max-height` are used similarly to the *-width properties.  

*Note*: If width is specified, padding and margin are also added (see below).

### Overflowing Content

Content can "spill over" from `min-width` and `min-height` settings of boxes.
By default the browser will allow the content to "spill" into other portions of the document or window.  
Properties `hidden` and n`scroll` can be set to tell the browser to handle the overflow more neatly.  

Hidden: Hides all content when an overflow is detected.  
Scroll: Overflow content is moved and a scrollbar is added to allow the user to scroll the content to read/access it.  

Older browsers used to shrink the font size when an overflow situation would otherwise occur. This is a good reason to use hidden or scroll to work around these back-level issues.  

### Border Padding Margin

These properties define the edge, inside edge, and outside edge of all sides of a box.  

- `padding`: Provides releif between the *content* and the *border*.  
- `border`: Every box has a border, and it can have `width: 0px` which makes it not visible, or visible with larger px sizes.  
- `margin`: Provides a gap between the *border* and other *boxes* or *elements* that are around it.  

Whitespace plays an important part is page readability and useability, so use these properties to your advantage.  

There are additional Border property settings:

- `border-width`: thin, medium, thick.  
- `border-style`: solid, dotted, dashed, double, groove, ridge, inset, outset, hidden.  
- `border-color`: colors can be set using rgb(), common color names, and other syntax.  

These and other settings can be 'shorthanded' to put all into a single line of the element properties:

``` html
head {
  border: 4px solid blue;
}
```

Borders actually have four sides, and these can be configured all as one, two at a time, all four simultaneously, or all four individually:  

- `border-width: thin medium;` causes the top and bottom border lines to be 'thin' and the left and right border lines to be 'medium'.  
- `border-style: dashed, solid, groove, ridge;` where these properties are applied in this order: TOP, RIGHT, BOTTOM, LEFT.  
- `border-top-style: ...; border-right-style: ...; border-bottom-style: ...; border-left-style: ...;`  
- `border-color: blue red white green` for colors.  
- `padding-top: 2px; padding-bottom: 4px;` for custom padding of the top and bottom of the box.  
- `margin-left: 40px;` for custom margin on the left side of the content.  

*Note*: Padding and Margin also support shorthand notation of just 2 values where the arguments represent top+bottom, and left+right, respectively.  

### Centering Content

Requirements:

1. Set the width of the box.  
2. Set the left-margin and right-margin to 'auto'.  
3. Older browser set: Add 'text-align' property but remember it is inherited by child objects.  

### Change Inline and Block Properties

The `display` property can be set to change the inline or block properties of elements.  

- `inline`: Causes the element to position itself in-line with the content.  
- `block`: Causes the element to position itself as a separate block between content.  
- `inline-block`: "Causes a block-level element to flow like an inline element while retaining other features of a block-level element." *[Duckett, pg.317]*  
- `none`: Causes element to not render on the document.  

*Note*: There is also a `visibility` property that can be set to 'hidden' or 'visible', rather than using `display: none;`.  

A wonderful example from *[Duckett, pg.317]* causes list item elements to list horizontally (inline) rather than vertically stack (block-level):

```html
<style>
  li {
    display: inline;
    margin-right: 10px;
  }
</style>
```

### Border Images

This property allows customizing a border, so the developer doesn't have to rely on the built-in `border-style` settings:

- An image can be applied to the border.  
- The image is repeated, once for each side (T, R, B, L) and for each corner between the sides.  

Three property settings are required to make this work:

- The URL of the image.  
- Where to 'slice' the image.  
- How to render the edges:
  - `stretch`  
  - `repeat`  
  - `round`  
- `border-width` greater than zero.  

Earlier browser versions of Chrome, Firefox, and Safari will need the following to render properly:

- `-moz-border-image`  
- `-webkit-border-image`  

### Box Shadows



## JS Book Chapter 2 Notes


## JS Book Chapter 4 Notes

From Switch Statements section onward.  
