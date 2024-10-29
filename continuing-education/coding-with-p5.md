# Coding with P5

## Table of Contents

- [VSCode Interviews Dan Shiffman](#vscode-interviews-dan-shiffman)
- [How To Use P5 With VSCode](#how-to-use-p5-with-vscode)
- [About P5](#about-p5)
- [Footer](#footer)

## VSCode Interviews Dan Shiffman

Host: Olivia Guzzardo @OliviaGuzzardo

Presenter/Guest: Daniel Shiffman @shiffman

- university instructor at NYU (ITP/IMA).
- publishes online coding tutorials.
- mostly geared toward beginners.
- producing content for ~10 years.
- Tools: P5.js [p5js.org](p5js.org) by [The Processing Foundation](processing.org) which is built on top of Java and JS.
- The Coding Train: Dan's website with tutorials, challenges, link to a Discord server, etc.
- Book: [Nature of Code (2nd Edition)](https://nature-of-code-2nd-edition.netlify.app)

"Express yourself through code"

## How To Use P5 With VSCode

Within `index.html`:

1. Reference the P5js CDN within a script tag.
2. Also reference a local js file (e.g. `scetch.js`) in a separate script tag.

Using Libraries:

1. Install P5.vscode Extension by Sam Lavigne.
2. Open Command Palette and type ''.
3. Point to an existing directory (or create a new one) where the project should be initialized.
4. A new VSCode instance opens.
5. Verify file system layout as follows (see example below).
6. Open `sketch.js` to start coding!

```text
root
| Libraries
| \p5.min.js
| \p5.sound.min.js
|
| \index.html
| \jsconfig.json
| \sketch.js
| \style.css
```

## About P5

- The draw loop: Continuously draws the page based on inputs within the `draw()` function.
- Install LivePreview Extension to see immediate results (P5js just runs in a web page DOM).
- P5 focuses on Accessibility e.g. `Describe()` enables visual representations of what is happening on-screen.
- Changing the visual design in P5 is really a matter of selecting a different vector object. Dan's example was changing circles to text.

## Notes On 2D Primitives

A fairly light-weight brain-dump and "whoops I'm gonna want to remember that" items.

- `circle`: Set an x,y location and a diameter. _Not radius_!
- `ellipse`: Set an x,y location and w (width) and h (height) of the ellipse. Skip `h` and it will default to same as `w` (like Circle()). Negative values are not processed and instead considered an empty parameter. When using WebGL mode, add parameter `detail` which is an Integer indicating the count of `vertices` to use to build the ellipse (max 50).

## Notes on Rendering

A light-weight section of notes I felt were important to write-out while learning P5.

- If coloring the `background(color)` along with other on-canvas objects, be sure to _call `background()` first_ before loading other object, otherwise they will _not be visible on screen_ when the `draw()` function is executing.
- `createCanvas(width, height, WEBGL, canvas)`: Only use once within a `setup()` function. Width and Height arguments are actually optional, defaults are 100 for both. Only use `WEBGL` parameter if browser supports WebGL Mode. `canvas` (optional) is an HTMLCanvasElement to use for the sketch.
- `resizeCanvas(widnowWidth, windowHeight, noRedraw)`: Define a new width and height for the canvas. `noRedraw` is boolean, defaults to false, indicates whether to delay calling `reDraw()` function.
- `preLoad()`: This is a lifecycle event handler. Guarantees these function calls complete before rendering begins: `loadImage()`, `loadFont()`, `loadJSON()`, `loadModel()`.

## Other Reminders

- `floor(number)`: Concatenates a Number to it nearest _lower_ whole number. Any Number type or function that returns a number type can be set as the parameter.
- `map(value, start1, stop1, start2, stop2, withinBounds)`: Maps a value within range start1 to stop1, into the range start2 to stop2, returning the remapped number. `withinBounds` is boolean, defaults to false. When set, it ensures an out-of-bounds `value` is mapped to an in-bounds remapped number.
- `noise(x, [y], [z])`: Tunable natural-seeming random number generator using Perlin Noise algorithm. Returns floating-point numbers between 0 and 1. Arguments define the 'point in space' that _tune_ the output.
- `noiseDetail()`: Further adjust the Perlin Noise output using 'octaves' and 'weight' to steer the noise quality.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
