# How to Build a Responsive Website without JavaScript

An NDC Oslo presentation titled "Your website does not need JavaScript", NDC Oslo, 2024.

Presenter: Amy Kapernick, Web Developer, Perth, AUS, [amykapers](amykapers.dev)

## Table of Contents

- [Non-Building Blocks](#non-building-blocks)
- [Building-Blocks](#building-blocks)
- [Anchor Links As Responsive Design](#anchor-links-as-responsive-design)
- [Accordians Using the Details Element](#accordians-using-the-details-element)
- [Form Validations](#form-validations)
- [CSS Tricks](#css-tricks)
- [References](#references)
- [Footer](#footer)

## Non-Building Blocks

What will _not_ be used:

- JavaScript
- Build Tools
- NPM Packages

## Building-Blocks

What will be used:

- HTML
- CSS

## Anchor Links As Responsive Design

Goal: Create an SPA with multiple tabbed pages using Anchor links and CSS.

Use Content Targeting:

- Use an Anchor Tag aka Link Element. These link to websites, files or resources, or _to an ID within the current page_.
- Use the `target` property of an element to get or update that elements' attributes.

```html
<html>
<head>

</head>
<body>
  <header>
    <nav>
      <a href="#home">Home</a>
      ...
      <a href="#contact">Contact</a>
    </nav>
  </header>
  <main>
    <section id="home">
      ...
    </section>
    <section id="contact">
      ...
    </section>
  <main>
</html>
```

```css
section {
  display: none; // hide this parent element

  &:target { // ampersand causes affect to apply to parent
    display: block; // show the parent element
  }
}
```

The Target Pseudo Selector:

- Supported in many browsers (wide-ranging support).
- _Not_ great for accessibility!
- [MDN: CSS Pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_pseudo-elements) and their Selectors.

The [Nesting Selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Nesting_selector):

- Used with CSS Nesting such as `element { property: style & childEl { proprty: style }}`.
- States the relationship between parent and child rules.
- Rule selectors are made relative to the parent element.
- Applies to the parent _not the child rule_.

Normally, a nested CSS Selector rule would apply to the _child_ of the parent element in the nested CSS. Use of `&` causes the rule to apply to the parent _given the parent element and child attribute/rule setting_.

## Accordians Using the Details Element

```html
<details>
  <summary>Accordian Item Summary</summary>
  <p>Accordian Item content</p>
</details>
```

Browser Support:

- Pretty good browser support.
- Accessibility support is there.

## Form Validations

Required Fields:

- Use the `required` attributes to the input element.
- _Not_ always a great idea (think through what elements _truly are required_).

Data Format:

- Validate this using specific input fields i.e. "date", "time", etc.
- Input field "patterns" can be used to let user know the desired format.

Browser Support:

- Fairly wide support.
- LImited validation capabilities. JavaScript can be used to bolster these by using native browser errors, adding messages, etc.

## CSS Tricks

### Nesting

Generally, Pre-Processors are used to make this simple.

Lately, CSS has enabled nesting to enable nesting.

Support:

- Came out in 2023 but is supported in the _big four_ major browsers.
- Too new to provide wide user coverage.

### Range Slider

Apply these attributes to `input` elements:

- `type`: Set to 'range'.
- `min`: Set the minimum value in quotes i.e. '0'.
- `max`: Set the maximum value in quotes i.e. '9'.
- Does _not_ have any UI labels on its own.

The `has` pseudo-selector:

- If the element _has_ another element (add constraints such as `:nth-child()`).
- Example: `div:has(p:nt-child(1)) { --chilren: 1; }`

Amy configured a complicated

Support:

- Input of type Range has been around sunce 2012.
- Data List (data labels) has been around since 2018 except FF is fairly new.
- `has` selector: Generally 2022 (FF: 2023).

### Testimonials

Testimonial Slider: Usually these are rendered as a 'slider' UI, showing multiplt testimonial cards, often automatically.

```html
<input type='radio' id='t_1' name='testimonials' />
<label for='t_1'>Quote 1</label>
<blockquote>
  <!-- quote -->
</blockquote>
```

Use Input type `radio` to make a selectable UI element.

Apply CSS to the `testimonials` element:

```css
.testimonials {
  display: grid; // layout
  grid-template-rows: 1fr auto; // resizable sections
  grid-template-columns: 1rf repeater(var(--num_test), auto) 1ft; // ad spacing for each column data
  justify-content: center;

  &:has(blockquote:nth-of-type(1)) { // count quotes
    --num_test: 1;
  }
  ...
}

blockquote {
  grid-column: 1 / -1; // across end-to-end of display
  grid-row: 1 / 2; // at the end display on the second row
}

label {
  order: 2;
  grid-row: 2;
}
```

Hide all quotes so they can be selected later:

```css
blockquote {
  ...
  pointer-events: none;
  opacity: 0;
}

input[type='radio']:checked {
  & + label + blockquote {
    opacity: 1;
    pointer-events: auto;
  }
}
```

Leverage `before` and `after` pseudo-elements to label the block quotes nicely:

```css
label {
  ...
  position: relative;
  cursor: pointer;

  &:before, &:after {
    height: 20px;
    width: 20px;
    border-radius: 50%;
    border: 2px solid var(--green);
  }
}
```

Add "selected" styling to the labels:

```css
label {
  ...
  &:after {
    background: radial-gradient(
      circle, var(--green) calc(100% - 6px),
      transparent calc(100% - 6px)
    );
    position: absolute;
  }
}
```

Relatively new (less than 5 years) Selectors:

- HAS Selector (2022, 2023).
- NOT Selector (2015, 2020, 2021).
- GRID: Around since 2017, has GT 90% support.

Warnings:

- Avoid using Form Inputs for purposes that they were not intended.
- Add Aria Labels to help screen readers understand (and state) the context of the elements.

### Toggle Switch

This segment was very involved, and included a large amount of CSS (much like the previous topic).

Amy also discussed using the `:has` pseudo-selector to toggle light and dark mode, using `:before` and `:after` selectors in conjunction with `:has`.

In summary, it was not a great solution because:

- Not Accessible ready.
- Also designs Form Inputs to be used in a way they were not designed.

### Image Carousel

An Image Carousel layout can be broken down into 4 elements:

- `input` of type 'radio' with a 'value' and 'id' set, and the `checked` attribute.
- `label` element with a 'for' attribute pointing to the the radio input, with label text content.
- `div` element with a class attribute to CSS assignment, application.
- `img` element with src attribute to a valid image and alt attribute for accessibility.

How is this displayed and styled?

```css
.carousel {
  display: grid;
  grid-template-columns: 4em 1fr 4em;
  grid-template-rows: 300px;
  grid-template-areas: 'previous image next';
  overflow: hidden; // do not overflow the page
  max-width: 100%;
}

.image {
  grid-area: image; // see grid-template-areas values
  opacity: 0;
}

label {
  display: none;
}
```

Find a radio input that is checked, the label after it, and the `image` class after that, and set the opacity to '1':

```css
input[type='radio']:checked + label + .image {
  opacity: 1;
}
```

Check if none of the radios have been checked within the carousel, and get the radio input after that, the label after that, and the image after that, and set its opacity to '1':

```css
.carousel:not(:has(input[type='radio']:checked)) {
  & input[type='radio']:first-of-type + label + .image {
    opacity: 1;
  }
}
```

Add Controls by finding the radio button that is checked, get the label next to it, get the image next to that, then get the radio button next to that and the label next to that, assign its display to block, set grid-area to 'next', and add the :arrow-right: emoji as the content:

```css
inptu[type='radio']:checked + label + .image + input[type='radio'] + label {
  display: block;
  grid-area: next;
  
  &::before {
    content: ':arrow-right:';
  }
}
```

Do a similar thing to find the 'previous image' to place the :arrow-left: emoji.

Support and Best Pracrtices:

- CSS Grid has good browser support.
- HAS Selector browser support is not as good as Grid.
- Image Carousels are _not good_ for performance.
- Image Carousels are _not good_ for accessibility.
- Turn off animation based on media query to check for 'reduced motion' or 'no-animation' settings on their system.

_Instead_: Use Gallery or something other than an Image Carousel.

### Items to Review

- [MDN: Pointer-Events](https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events): Sets the circumstances under which a graphic element can become the `target` of pointer events :arrow-right: Auto, None, Stroke, or Fill.
- [MDN: Block Quotation Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote): Indicates enclosed text is a quotation by rendering with indentation (which can be changed). Related [MDN: Cite Attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote#cite), used to link to quotation source, and the [Cite Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/cite), used to display citation text.
- [MDN: Grid Display](https://developer.mozilla.org/en-US/docs/Web/CSS/grid), shorthand property that sets all explicit and implicit Grid control elements in a one-liner. Constinuent properties (set and assumed by `grid`) are `grid-auto-columns`, `grid-auto-flow`, `grid-auto-rows`, `grid-template-areas`, `grid-template-columns`, and `grid-template-rows`.
- [MDN: Functional `:Has()` CSS pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:has) represents an element where any of the relative selectors passed-in match at least one element when anchored against _this_ element.
- [MDN: `:Not()` CSS pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/:not) represents elements that _do not_ match a list of selectors. Aka 'negation pseudo-class'.
- [MDN: Position CSS Property](https://developer.mozilla.org/en-US/docs/Web/CSS/position) sets how an element is positioned in a document. `Top`, `Right`, `Bottom`, and `Left` properties deterine final location of the element.

### Final Comments

JS is useful, but is it really necessary?

- JS _can_ make websites better, but _is not always_ the answer.
- Can you do the same with HTML intead? Some elements already exist or can be created without much effort, rather that relying on a module.
- Can you do it with CSS? Animations in JS can sometimes be replaced with CSS.
- If the website is tracked for SEO, etc, JS is most likely necessary.
- Is JS being written for _good_ or for _evil_? _[Amy Kapers]_

## References

Check out Amy's live site at [nojs.amyskapers.dev](https://nojs.amyskapers.dev).

To learn more about Amy and her talks, see [Kapers.dev](https://kapers.dev).

## Footer

- Return to [ContEd Index](./conted-index.html).
- Return to [Root README](../README.html).
