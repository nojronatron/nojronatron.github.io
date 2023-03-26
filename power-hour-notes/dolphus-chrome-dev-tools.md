# Chrome Dev Tools for Power Users

Presenter: Titus Dolphus, Web Developer.

FE Engineer at Magenta Technologies.

## Content Notes

Developers, cyber-security experts _are_ power users!

Chrome Developer Tools are used heavily in the industry.

- Inspect, debug, and optimize web pages.

What about other browsers tools?

- Chrome has the largest market share.
- Many of the same tools are included in Firefox, etc.

### Tools

Element Inspector:

- Many javascript and css files in code make it difficult to track down what code needs to be edited to make a change.
- DevTools allow changing look and feel (HTML and CSS) on the page.
- Hover-Popup shows some highlights of the highlighted element attributes and styling.
- Hover, Focus, and Active states are not shown in the Hover-Popup. DevTools has a button e.g. `:hov` to force a state on a highlighted element.
- Color Picker within the DevTools Style view changes the applied color on the selected element in real time. Actual code is not changed.
- Simulate Mobile and other viewport experience using Device Toolbar. Dimensions are preset, but can be edited with viewport sliders or typing in actual values.
- Inspector changes are overwritten when the page is refreshed. Use Inspector as a preview, and also to find the file and codeline where Style is applied, etc.

Console:

- Adding code in the Console actually _adds code to the DOM_ until the next refresh.
- Adding code helps experiment with ideas without editing code directly. Once Console code works, then try adding to actual Code.
- Nothing in the Console goes to any other users.

Sources:

- Includes a Code Editor (JavaScript and CSS).
- Can debug executing code.
- Changes are NOT saved to your code. Refresh restores to the built-code version.
- Use to experiment _directly in the code_ already loaded in the DOM, without affecting IDE code.
- Can store code as Snippets! Snippets are not removed when page is refreshed.

Network:

- Displays all HTTP-based requests and responses when a page loads.
- Load-times are tracked.
- View information on-the-wire.
- Check Headers for unexpected targets in request.
- Check Payload for requests with unencrypted data, when it should be encrypted.
- Network tool _must_ be selected when the Request happens otherwise data is not captured.
- Use Preserve Log button to store Network trace info.
- Select the ALL view to see every file that is fetched during a page load. This is a good place to look for XSRC and other potential issues.

Lighthouse:

- Design, Dev, and SEO can have conflicts here with various goals including look-and-feel vs inter-web optimizations.
- Lighthouse compares results to results compiled through Google.
- pagespeed.web.dev: Test the speed of a website live of the internet.
- Lighthouse get similar data to pagespeed's website.
- Drill-down into the report entries to get advice on where the problems are and how it came to the report conclusions.
- Pagespeed won't work on non-indexed sites e.g. Dev or Test, however

## Resources

YouTube: Fireship "the best dev youtube channel ever" _[Titus]_

[PageSpeed](https://pagespeed.web.dev)

### Keyboard Shortcuts

Launch Dev Tools for Chrome:

- Windows: CTRL SHIFT I
- Mac: OPT CMD I

Inspector Panel: Zoom In

- Select Elements tab and press CTRL +

Dev Tools Command LIne:

- CMD SHIFT P

## Footer

Return to [PPH Index](./pph-index.html)

Return to [Root README](../README.html)
