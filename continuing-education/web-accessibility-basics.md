# Web Accessibility Basics

MSFT Learn training notes in the ASP NET Core training Learning Path.

## Learn about Accessibility

- Tools that users use to browse web pages.
- Tools developers use to ensure accessibility.
- Skills for ensuring pages are accessible.

### Accessibility Tools for Users

Screen Readers:

- Commonly used.
- Users with vision impairments.
- Reads a page from top to bottom audibly.
- All text is conveyed directly like it is in the browser.
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

Responsive Design:

- Necessary for managing the look and usability of a page when tools like Zoom are used to assist.

### Accessibility Tools for Developers

Color-blindness affects nearly 1:10 adults.

Contrast Checkers:

- W3C established a [rating system for color contrast](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
- Adobe Color: Interactive tool for testing color combinations.
- Color Safe: Generats text colors based on selected background color.

Compliance Checkers:

- Edge: WCAG Color Contrast Checker.
- Firefox: WCAG Contrast Checker.
- Chrome: Colour Contrast Checker.

Applications:

- Colour Contrast Analyser (CCA).

Lighthouse:

- Google created tool for analyzing websites.
- Examines page for SEO, load performance, and other best practices.
- Analyzes page accessibility and provides an overall score with suggestions for improvement.

### Accessibility of Links and Images

Link Text:

- Avoid adding the link URL. Screen readers will read this aloud that that is rarely necessary.
- Add more information that 'click here' because Screen Readers have a feature to just read links aloud, and the _context_ of each link is important when these are read out serially.
- 'Click' is a specific _mouse action_ or event, but not all visitors will be using a device that 'click's.
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

## Resources

Review [WebAIM](https://webaim.org/techniques/keyboard/) for tips on keyboard-nav friendly development techniques.

[Web Development for Beginners](https://github.com/microsoft/Web-Dev-For-Beginners) curriculum by Azure Advocates.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
