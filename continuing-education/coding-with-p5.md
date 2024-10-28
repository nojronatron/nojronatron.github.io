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

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
