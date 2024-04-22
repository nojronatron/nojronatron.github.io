# Read Class 43 OSS Contributing

## Resources

[First Timers Only](https://www.firsttimersonly.com/)

GitHub [open-source repo](https://github.com/open-source)

Clearcode on [what motivates a developer to contribute to OSS?](https://clearcode.cc/blog/why-developers-contribute-open-source-software/)

GitHub [Search for "a good first issue"](https://github.com/search?q=label%3Agood-first-issue+archived%3Afalse)

CallForCode.org [Help Solve the World's Greatest Challenges](https://callforcode.org/)

## First Timers Only

Scott Hanselman and Kent Dodds put together this website (and efforts behind promoting the OSS community). Links to resources for how to get starting contributing to OSS projects, as well as tips for OSS project owners to make their projects easier to find and work with especially for new contributors.

There are multiple links to OSS contributing resources and tips, as well as a link to a GitHub APP that will make "good first issue" markers easier to apply.

## Motivations To Contribute to OSS

> A great way to practice coding, everyday!

> Learn by working on a live codebase.

> Gain valuable feedback on your code and development processes.

> More experienced developers can concentrate on more difficult or complex issues, leaving simpler issues for less experienced devs.

> Some companies require OSS participation as a gating factor to employment.

> Gain experience reading and writing code, and finding bugs.

> Peer recognition: Builds professional network and provides a means for others to see and understand a developer's skill level and passion for software development.

> Prospective employers can easily skim OSS code in public repositories and gain insight into a candidate's activities, interests, and capabilities -- their potential value-add.

> Even non-code oriented contributions are encouraged with OSS. For example: Feature suggestions, finding bugs, and updating or improving documentation.

## Call For Code

CallForCode.org has partnered with IBM and many other tech companies to promote developing solutions for the greater good.

Global projects that promote and enable diversity, equality, and inclusion are highlighted.

CallForCode provides assistance to contributors, and there are also pay-out awards for completing projects within the scope of their call to actioni initiatives.

## Interesting Contrib Opportunities

- [x] Sequence TubeMap by VGTeam: [Form fields are weirdly wide now](https://github.com/vgteam/sequenceTubeMap/issues/149)

> A reference to a bootstrap variant the above project uses [reactstrap](https://reactstrap.github.io/?path=/docs/components-forms--input)

> Create React App [Getting Started Doc](https://create-react-app.dev/docs/deployment/)

## IVG Sequence Tube Map

This project is a React App that uses Yarn (instead of NPM), react-strap, CSS, and some other styling frameworks to produce an appealing UI where scientific gene-folding data can be uploaded to the site and a "tube map" will be rendered on-screen.

There is an open Issue marked as a Good First Issue that mentions an unexpected layout problem with some of the Form Inputs:

- Expected: Form fields should not be so long (beyond the rest of the content).
- Expected? Form fields should be in horizontal row across the screen, or 1-2 rows on desktop screen sizes?
- Actual: Form fields are stacked on top of each other and span the width of the screen?
- If the viewport size is reduced, should the form fields stack vertically?
- What if the form fields lengths are shrunk but are stacked vertically instead?

After a little research I found some areas that need some exploration to determine root cause:

- A major version update occurred in several style and layout orientated packages in a recent PR, which sprung the creation of the GH Issue.
- Inconsistent use of styling elements and properties between components.
- A mix of CSS, reactstrap, react-bootstrap, and react-select were applied, which could have unexpected side effects.
- Duplicate styling framework components applied between parent and child React Components could have unexpected side effects.

### Root Cause Analysis

1. Why are the input boxes (drop-down/select and text inputs) stacked on top of each other vertically instead of side-by-side as one of the codebase owners expected.
1. Why have the Input elements in HeaderForm Component rendered within a Container structure (i.e. a Grid) that includes Rows and Cols that have built-in and custom CSS applied?
1. Why are some components that are rendered within the HeaderForm Component using different frameworks for styling?
1. Why aren't there constraints to the width of the input elements, such as tighter column spacing, or direct CSS application impacting their size?
1. Why isn't there a specification document for the layout of this "main page" of the Application?

Some interesting discoveries through investigation:

- Downgrading bootstrap, reactstrap, and react-select by removing the lock files and editing package.json to point to pre-PR versions then rebuilding did not have a significant effect on the stated problem.
- Various bootstrap-ish frameworks apply specific widths, merging, and display types through M=margin, P=padding, D=display, W=Width etc are used, which is fine, just needed to review what they were doing.
- HeaderForm.js on line 466 enforces `<Container fluid = {true}>` which *definitely impacts* the length and arrangement of the input elements. Removing this shrinks-down the form fields but Warning "vg view failed" display still spans entire viewport width, which is HeaderForm.js line 427.
- `{errorDiv}` needs to be inside the root container of the return statement (HeaderForm.js at about line 464).
- SelectionDropDown.js line 33 forces a minWidth of 100% and removing that setting causes the *options* in the drop-down to be shortened but the parent drop-down is still super wide, so that setting *should not be edited* as far as I can tell.
- SelectionDropdown.js has very deep, programmatically assigned style properties on line 11 `const styles={...}` could this be forcing the drop-downs to be longer than necessary (but, see previous bullet, and there there isn't evidence it is making a positive difference when adjusted).
- There is a nesting of input elements: Some of them do not appear unless a parent element selects a particular option item, for example: Selecting 'File' from the top drop-down will change-out the following input elements with those necessary to upload or select a file. This is just an effect of the flags i.e. `mountedFilesFlag && ( {JSX...} )`
- Form elements are spread across components: HeaderForm.js and a few others (see React Hierarchy depiction, below). FormGroup elements are not implemented and, if done correctly, *could* impact display for force in-line, if all placed within the same FormGroup or a specific attribute that has this effect.
- App.css rule `.dropdown` has a property `width: 100%;` that could be forcing drop-down elements to be too long??

### ACP PR Solution 17-July-22

The Header information was overflowing the container in main view. There are several awkward rendering issues, none of them severe, but the main one was a massive overflow.

It was not entirely clear whether the repo owner wanted the form fields to be horizontally (in-line) or not, and attempting to make them that was had some complexities in the way the CSS is utilized, and also how the form fields operate as there are a bunch of dependencies. For example, selecting a different data source actually changes which fields are displayed, and each one has a slightly different implementation when it comes to layout and design.

The team working on this project utilized multiple CSS/SCSS UI design packages and there are implications to using those that made reorganizting the form fields very difficult. I was able to get the form fields to shrink-down to within the general overall page-width without otherwise impacting the look-and-feel.

I'n not convinced that changing the layout of the form fields to in-line will be easy to do, but I might take another stab at it when I get some more React and Bootstrap experience under my belt.

### General Hierarchy

The React App Components in this project are arranged (best I could tell) as follows:

![SVG Tubemap React Component Hierarchy (reverse-engineered)](./images/TubeMapReactComponentHierarchy(reverseEngineered).jpg)

![SVG Tubemap React Site Rendering (assembled from React Components)](./images/TubeMapReactSiteRendering(pseudoAssembledFromReactComponents).jpg)

### Build And Test

They recomment compiling VG in order to import sample (and actual) data for dev and test.

Since I am focusing on a UI design issue, I won't worry about VG right now.

1. Fork the repo.
1. Clone to local.
1. CD into project
1. 'yarn install'
1. 'yarn build'
1. 'yarn serve'

Dev and Test Cycles

1. For most changes, it is necessary to re-run 'yarn build'.
1. In order to render the website on your local browser, you will need to run 'yarn serve'.
1. Open your browser to localhost:3000 and the main page should render.

*Note*: Review the project [README](https://github.com/vgteam/sequenceTubeMap) for additional tips of dev and test deployments on local.

*Note*: If you haven't built since the last change, your changes might not take effect!

## OSS Contribution Accepted

The [PR](https://github.com/vgteam/sequenceTubeMap/pull/173) containing my contributed fix was merged and closed in September 2023! :tada:

## Footer

Return to [Root README](../README.html)
