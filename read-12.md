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

Article Source: *[SARA VIEIRA, freelance Web Designer and Developer](https://iamsaravieira.com/)  

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

[MDN > Canvas API > Drawing Shapes with Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)  

[MDN > Canvas API > Applying Styles and Colors](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors)  

[MDN > Canvas API > Drawing Text](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Drawing_text)

[Back to index in readme](./README.md)