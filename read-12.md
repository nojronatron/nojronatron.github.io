# Notes From Various Resources on ChartJS and Canvas API

## WebDesignerDepot Article on Chart.js

[WebDesignerDepot.com article on chart-js](https://www.webdesignerdepot.com/2013/11/easily-create-stunning-animated-charts-with-chart-js/)  

Rather than using tables to display data, use charts!  
ChartJS makes creating and styling charts much easier.  

To get started with Chart.js:

1. Download it.
2. Copy Chart.min.js into your css folder.
3. Import Chart.min.js into your html page.

The `<canvas>` element is used to set a new chart on the page.  
Use `<script>` element to grab data for the chart.  
Associate the script data with canvas element via the id attribute in the canvas element.
Use a DOM query to find the chart element and store in a local variable.  
Instantiate a new Chart object using DOM query element as a parameter.  
Chart options are JSON data to set values and colors.
Line, Pie, and Bar charts were shown as baseline examples.
Chart animation is fairly straightforward, just set a property or two.

Article Credit: *[SARA VIEIRA, freelance Web Designer and Developer](https://iamsaravieira.com/)  

## Chart.js Home Page

[CharJS.org Docs](https://www.chartjs.org/docs/latest/)  

Chart.js is supported by most modern browsers, including:

- Chrome, Edge, Firefox, and Safari  
- Major mobile browsers  

*Note*: The dev team used [BrowserStack](https://www.browserstack.com/) to test the code against many browsers.  

IE 11 is no longer supported.  

Chart.js has a Slack channel for discussion, GitHub repo for bugs and commit/pr'ing, and the project is well documented and easy to follow.

Animation features allow fly-in or 'bouncy' charts. Much more fun than the status quo.  
Resizing/responsiveness is possible however a specific set of configurations must be followed to avoid blurry charts or render errors.

## Mozilla Developers Network Canvas API Basic Usage

[MDN > Canvas API > Basic Usage](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage)  

Think of the `<canvas>` element as an `<img>` element but without src or alt attributes.  
Width and Height are the only attributes.  
CSS Styling and DOM Manipulation can be acquired through Class or ID attributes.  
CSS Rules applied to a Class or ID or parent of the Canvas element do not change the Chart style, rather the container surrounding the chart.  
A closing tage is *required*.  
Apply alternate content by putting it between elements, i.e.:

```html
<canvas id='stock-chart' heigh='100px' width='100px'>Stock Chart is not available</canvas>
```

Two- and Three-dimensional chart renderings are available.  
To test for support, execute `canvas.getContext()` and use the result to render a canvas or something else.  
MDN has several minimalist examples that could probably be used as boilerplate.

## Mozilla Developers Network Canvas API Drawing Shapes

[MDN > Canvas API > Drawing Shapes with Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)  

The drawing 'grid' (Coordinate Space) is how the canvas drawing space is described.  
Coord (0,0) is at the top-left corner, so (x,y) pixels are targeted accordingly.  

Two shapes are supported:  

- Rectangles: These can be filled, outlined, or transparent.  
- Paths: Line segments. Stroke() is the brush stroke creating the line; Fill() draws a solid shape by filling between lines.  

Draw Triangles using LineTo() and MoveTo().  
Draw other objects or free-form using Paths and Arcs.  

MoveTo() moves the 'pen' to a new location, to start drawing elsewhere on the canvas.  

Use Loops to make many drawings!  
Make quadratic or bezier shapes and patterns!  

## Mozilla Developers Network Canvas API Style and Color

[MDN > Canvas API > Applying Styles and Colors](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors)  

Color is added using `fillStyle()` and `strokeStyle()` methods.  
*Note*: These methods are 'sticky', meaning once set, following drawing commands will use them, until the methods are changed again.  

Transparency is possible using globalAlpha property or by assining a semi-transparent color to the stroke/fill style.  
RGBA() fillStyle() properties provide a bit more control over the hue and brightness.  
Lines can be styled with:  

- Width
- Dashed or solid
- Cap: how the end of the line is styled
- Join
- setLineDash() and lineDashOffset()
- gradients: linear, radial and conical
- various 'patterns'

## Mozilla Developers Network Canvas API Drawing Text

[MDN > Canvas API > Drawing Text](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_text)



[Back to index in readme](./README.md)