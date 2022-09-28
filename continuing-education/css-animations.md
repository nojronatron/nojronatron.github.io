# CSS Animations

Notes taken while learning how to animate website elements using CSS.

## MDN

## Web Dev Simplified

[Learn CSS Animation in 15 Minutes](https://www.youtube.com/watch?v=YszONjKpgg4)

Two ways to animate:

- Transition property: Simple, easy to use, but not necessarily smooth.
- Animation property: More complex, better multistep animation capabilities.

### Transition Animation

Where to apply it?

- Do *not* apply it on the `:hover` pseudo property.
- Instead put it in the base class (className/ID) for the target element itself.

Transition shorhand => delay, duration, property, timing-function. Enter one or all of these in the shorthand Property entry, rather than typing out up to 4 lines of properties.

Smooth transition: `transition: transform 1s;` => Works on `translateX()` and other properties to smoothly transition between initial and ending "state".

timing function: Linear | ease-in-out |

Ease-in-out can be edited! Use the Inspect tool, find the timing function property, click on the function icon, and an editor appears with a bunch of built-in functions, and custom functions can be defined using the visual editing tool!

### Animation Syntax

Minimal short-hand to get animation to work:

1. Use the word `animation`
1. Set a custom name so it can be referenced.
1. Specify a duration.
1. Specify a timing function (ease-in, etc).

Keyframes are needed to set *steps*:

1. keyword `@keyframes`
1. Give it a custom name so it can be referenced.
1. Within the braces include the how far into the animation the transform (or other property) should be executed.

Note: Once keyframes is done, the element resets back to it's originally set values.

To solve this use `animation-fill-mode`: forwards | backwards | both | none | initial | inherit.

### Advice

VSCode provides help so slow down while developing CSS properties and use those intellisense prompts to help find the correct sub-properties, and settings.

## Footer

Return to [conted-index.md](./conted-index.html)
