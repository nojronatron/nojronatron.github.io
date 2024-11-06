# Web Accessibility Basics

MSFT Learn training and other notes regarding Web Accessibility.

## Table of Contents

- [Learn about Accessibility](#learn-about-accessibility)
- [ASP.NET Core Accessibility (MSFT)](#aspnet-core-accessibility-msft)
- [Special Elements and Attributes](#special-elements-and-attributes)
- [Resources](#resources)
- [Footer](#footer)

## Learn about Accessibility

- Tools that users use to browse web pages.
- Tools developers use to ensure accessibility.
- Skills for ensuring pages are accessible.

### Accessibility Tools for Users

Screen Readers:

- Commonly used.
- Users with vision impairments.
- Reads a page from top to bottom, audibly.
- All text is conveyed directly, as it is in the browser.
- Some have read-aloud features.
- Some have navigation features to simplify surfing websites.
- Rely heavily on Headings to find information and browse through a page.

Zoom (Windows, iOS, Mac):

- Static Zoom: Most common, controlled through keyboard shortcut [Ctrl] + [+] or by decreasing screen resolution, resizing entire page.
- Windows Magnifier: Built-in to Windows.
- ZoomText: Fully featured add-on to Zoom.

Screen Reader Tools:

- Narrator: Windows tool, included by default.
- JAWS: Windows app.
- NVDA: Windows app.
- VoiceOver: macOS and iOS. Installed by default.
- Talkback: Android screen reader (appears to be built-in).

Responsive Design:

- Necessary for managing the look and usability of a page when tools like Zoom are used to assist.

### Accessibility Tools for Developers

Color-blindness affects nearly 1:10 adults.

Contrast Checkers:

- W3C established a [rating system for color contrast](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
- Adobe Color: Interactive tool for testing color combinations.

Compliance Checkers:

- Edge: WCAG Color Contrast Checker.
- Firefox: WCAG Contrast Checker.
- Chrome: Colour Contrast Checker.

Applications:

- Colour Contrast Analyser [CCA](https://www.tpgi.com/color-contrast-checker/).

Lighthouse:

- Google created this tool for analyzing websites.
- Examines page for SEO, load performance, and other best practices.
- Analyzes page accessibility and provides an overall score with suggestions for improvement.

### Accessibility of Links and Images

Link Text:

- Avoid adding the link URL. Screen readers will read this aloud, which is rarely necessary.
- Add more information than just 'click here' because Screen Readers have a feature to just read links aloud, and the _context_ of each link is important when these are read out serially.
- 'Click' is a specific _mouse action_ or event, but not all visitors will be using a device that 'click's. See [MDN's Overview of Touch Events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events) for more information.
- Use the Title of the Link as the link text.
- Following good Link Text practice will also help with SEO.

### ARIA Attributes

ARIA: Accessible Rich Internet Applications

- Describe a link with `aria-label`.
- When semantic-HTML is not available, use ARIA to fill-in the context of the page layout and content: `aria-labelledby="a-parent-id"`, `aria-expanded="false"`
- Semantic HTML is preferred over ARIA but accessibility is the primary goal so both methods should be utilized as necessary.

### Alt Text for Images

Screen readers can't read contents of an image.

- Some use AI, but results might not be contextually accurate.
- Use `alt="descriptive text"` attribute of the `<img>` tag to provide the detail.

### Using HTML

HTML was designed to describe a page layout and provide space for content.

- Use the elements as they are designed.
- Use an `<h1>` and re-style it if necessary, rather than syling a `<div>` to get the desired effect.
- Stylized elements _only convey visual information_ rather than stuctural.

Best Practices:

- Use the correct HTML element for layout.
- Use the correct HTML controls for buttons and other interactive components.
- Avoid mixing hyperlinks and button-type controls.
- Use good visual queues: Avoid removing underlined hyperlinks and instead provide visual feedback when elements are hovered, clicked, or en/disabled.
- Leverage the keyboard: Pages should present content in a logical order for keyboard-only navigation. The [Tab] key will be used extensively for page navigation.
- Consider the natural flow for navigation throughout a page including tables, side bars, menus, and pop-ups/modals.

## ASP.NET Core Accessibility (MSFT)

### Inclusive Design

- Inclusivity means increasing user-base.
- Legal requirements (like governments and regulated industries) to meet compliance standards.
- Human rights. Help others gain full access to the internet.

### Screen Readers

- Built-in to most modern operating systems.
- Reads page from top to bottom.
- Conveys information similar to how the Browser does.

### Visual Impairments

- Users may prefer audible read-aloud.
- Other users may prefer magnified page experience.

### Design for Accessibility

- Modern browsers and web standards are designed for accessibility.
- Built-in elements designed to "just work" (so don't break it during development).
- Bootstrap contains ASP.NET Core templates: Support accessibility (although is not comprehensive).

### Structure

Again, using built-in HTML elements and their included attributes will provide a more accessible web UI without additional code:

- Input elements should be "typed" such as `<input type="button">`.
- Input elements can be marked with the `required` attribute, and styled accordingly such as `input:required { border-color: red; }` if wanted or necessary.
- Use `<form>` and its attributes to create a single, encapsulated form without having to write additional event handlers. Form `action` attribute saves the developer from having to write a specific event handler to send form data.
- Use `input type="submit"` with `onclick=()` handler attribute to handle form submission.
- Tab order is important, so designing the page with appropriate elements in a sensible order will provide a good experience for navigation by tabbing. Use `tabindex` attribute to set (or disallow) an element's tab order in the page tab sequence.
- Use `<details>` and `<summary>` elements as widgets that simplify showing or hiding additional content interactively.

### Accessibility Insights For Web

FastPass Tool:

- Checks for many accessibility requirements.
- Instructs developers on how to fix issues.

Assessment Tool:

- Also checks for many accessibility requirements.
- Provides how-to fix instructions for many common issues.

Other:

- Additional access to tools that help ID other accessibility issues.

_Note_: There is a Windows version of the tool, as well as the Chrome and Edge Plug-ins.

### Windows Color Filters

Windows 10 and 11 include Color Filters feature with color palettes that can make colors on the screen easier to see.

- `WinKey + X` :arrow-right: Settings :arrow-right: Accessibility :arrow-right: Color filters.
- Select a color filter set to deuteranopia, protanopia, tritanopia, grayscale, or inverted settings.
- Set a Keyboard Shortcut to enable/disable the color filters.

Select Color Filters to view your website (or App) to simulate varying degrees of color-sightedness.

_Note_: Using Colors on a form to indicate required fields might not be a good solution due to varying color sensitivity of visitors, and those that use a screen reader will not "see" the colors, therefore element attributes and other means should be used to convey that a field is required.

### Viewport and Zoom

Large monitors, small monitors, and mobile devices will cause the website to look different.

Some font sizes, paddings, or borders will make the page easier or harder to view and navigate.

Many users with sight limitations will use Zoom to 200% or more to be able to read text on your page.

Does the page accommodate these viewports and various Zoom settings?

### Screen Reader Accessibility Issues

- Screen Reader Options: Windows Narrator, JAWS, and NVDA all work on Windows. VoiceOver for macOS and iOS.
- Navigation, Headings, and Images are the three primary anchors to accessible content.
- Text, forms, search, and data tables must also be designed to be Screen Reader ready.
- Page Structure: The key to accessible page design. Use built-in elements to provide _semantic_ structure information: `header`, `nav`, `main`, `article`, `aside`, `footer`, `section`. Avoid relying solely on `div` as it has no semantic meaning for Screen Readers.
- Heading Elements `h1` et al: Provide a tree-like navigable structure to a website. Use headings elements for structure, and re-style them as needed for visual design.
- Primary heading `h1`: There can be _only one_. When read with a Screen Reader, a single `h1` ensures a simple, navigable web page hierarchy.
- Tab Order: Be default, web pages will usually have a reasonable tab order (L to R, Top to Borrom) but there are exceptions. Test your page to verify the Tab Order makes sense.
- Images: Use the `alt` element and provide succinct, descriptive text for what the image is when it is the subject matter of the content. If it is purely decorative, still include the `alt` attribute but leave it blank.

## Special Elements and Attributes

- `inert`: An attribute that causes an element and its descendants to become inactive and hidden from assistive technology.
- `focusgroup`: An attribute that enables using arrow keys to set focus to an element, among a group of elements.
- `<search>`: Semantic element to wrap a Search tool.
- `fieldset` and `legend`: Group related elements together, enhancing accessibility.

## Resources

[Inclusive Design Notes](continuing-education\inclusive-design-notes.md) taken while reading Inclusive Design 101 on Microsoft Learn.

[Accessibility Insights for Web](https://accessibilityinsights.io/docs/web/overview/).

Guidance and Tutorials from [W3C Web Accessibility Initiative website](https://www.w3.org/WAI/design-develop/).

Review [WebAIM](https://webaim.org/techniques/keyboard/) for tips on keyboard-nav friendly development techniques.

[Web Development for Beginners](https://github.com/microsoft/Web-Dev-For-Beginners) curriculum by Azure Advocates.

[Introduction to Web Accessibility](https://www.w3.org/WAI/fundamentals/accessibility-intro/).

W3C resource on [How People With Disabilities Use The Web](https://www.w3.org/WAI/people-use-web/).

[Inclusive Design](https://www.microsoft.com/design/inclusive/) by Microsoft.

[Accessibility Insights](https://accessibilityinsights.io/).

YouTube video [Introduction to Accessibility Insights for Web](https://www.youtube.com/watch?v=U6NY8Cxym5g).

MDN Web Docs: [HTML: A good basis for accessibility](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
