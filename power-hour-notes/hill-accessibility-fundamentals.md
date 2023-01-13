# Accessibility Fundamentals

## Introduction

Stephanie Hill

Code Fellows Grad

## Importance of Web Accessibility

Solutions are designed and developed for use by people with disabilities.

- Healthcare
- Government
- Services
- Education and Training
- Jobs and Career

Providing equal access and opportunity to a diverse range of people.

The U.N. defines accessibility as a *basic human right*.

- 1-in-5 of the Earth's population have disabilities
- Impact of disabilities varies and has changed with technologies
How to make accessibility a part of the software development process?

## Technologies and Innovation

Typewriters were standardized for support use by the blind and sight impared.

Smart-speakers and assistive technologies.

Texting 911.

Closed captions.

Think of accessibility technolgies as an 'electronic curb-cut'.

- Assistive Technolgies: HW or SW that enable use.
- Adaptive Strategies: Techniques that people with disabilities use to interact with the environment.

Common Tools

- Screen readers: Start at top of doc/website and read any text (in-line, alt, previews, navigation, etc).
- digital braille display: Tactile hardware input/output device.
- keyboard navigation: Common navigation strategy used by many people.
- speech input: Speech recognition to enable text input, command activation, links, etc. Mouse-grid overlays screen with zones 1-9, allowing speech to direct focus to a segment of the screen.
- closed captions: Textual version of spoken work within media, etc.

Software Helper Tools:

- VoiceOver
- ChromeVox
- Narrator
- NVDA
- MouseGrid

## Structural Fundamentals

Semantic HTML:

- a foundation for accessibility.
- common tools rely on this to help convey context and content to the user.
- by default, these enable keyboard-navigation interactivity.
- Headers, lists, form elements, links, Form elements, and anchor elements.
- div and other generic elements do NOT enable native interactive capability.
- Semantic elements provide 'free behavior' that supports accessibility.

Text Alternatives:

- Img element alt attribute: Short description of the image.
- Depend on the surrounding content.
- `<label>` Describe input elements. Use the `for=` attribute to match the id of the input element.

ARIA: Accessible Rich Internet Applications

- Can identify form controls.
- Supported by screen readers and other assistive technologies.
- Informaiton is NOT conveyed visually.
- Don't use to duplicate the content of the input element, or the type of element.

Keyboard Accessibility:

- *Visible* keyboard focus: Styles that show which element has focus and can be interacted with. Use "Focus State" to declare what is actionable.
- Appropriate tab order: Follow the visual order of reading a page such as Header, main nav, page nav, and then footer. Group like-content together. Avoid long-lists of clickable elements (think about how the user must navigate and select/click an element). Try SkipLinks.
- Avoid keyboard traps: Example: Tabbing through a drop-down list but it doesn't close afterwards, and no navigational alternative is provided.

Skip Link: Useful to help user jump over very long lists of links and information to get to where they might want to go.

```html
<header>
  <a href="#main" class="skip">Skip to...</a>
  <!-- content -->
</header>
<main id="main">
  <!-- content -->
</main>
```

There was also an example CSS class definition that supported hidden SkipLink.

## Tools for Testing Accessibility

Try testing functionality via your keyboard:

- Tab to all.
- Tab away.
- Tab order.
- Visual Focus.
- All functionality by keyboard.

Wave Evaluation Tool:

- Free.
- Browser Plug-in.
- Displays errors, ARIA, and other statistics.
- Errors are linked to exact place in code where the error occurs.

## Additional Resources

WCAG: Web Content Accessibility Guidelines.

Wave.wabaim.org

MDN Accessibility Docs.

A11ycasts with Rob Dodson (YouTube).

EdX W3Cx WAIO.1x Introduction to Web Accessibility (Free course on EdX).

## Other Notes

The "Accessibility Tree": Relates to accessibility and the structure of your site/user interface.

## Footer

Return to PPH [Index](./pph-index.html)

Return to [Root README](../README.html)
