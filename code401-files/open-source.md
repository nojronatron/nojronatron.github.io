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

- [ ] Sequence TubeMap by VGTeam: [Form fields are weirdly wide now](https://github.com/vgteam/sequenceTubeMap/issues/149)

> A reference to a bootstrap variant the above project uses [reactstrap](https://reactstrap.github.io/?path=/docs/components-forms--input)

> Create React App [Getting Started Doc](https://create-react-app.dev/docs/deployment/)

## IVG Sequence Tube Map

This project is a React App that uses Yarn (instead of NPM), react-strap, CSS, React-Bootstrap, and some other styling frameworks to produce an appealing UI where scientific gene-folding data can be uploaded an a "tube map" is rendered on-screen.

There is an open Issue marked as a Good First Issue that mentions an unexpected layout problem with some of the Form Inputs.

After a little research I determined the cause could be:

- A major version update occurred in several style and layout orientated packages, just prior to the Issue being created.
- Inconsistent use of styling elements and properties between components.
- A mix of CSS, reactstrap, react-bootstrap, and react-select were applied.
- Some duplicate styling framework components applied between parent and child React Components.

### Root Cause Analysis

1. Why are the input boxes (drop-down/select and text inputs) stacked on top of each other vertically instead of side-by-side as one of the codebase owners expected.
1. Why have the Input elements in HeaderForm Component rendered within a Container structure (i.e. a Grid) that includes Rows and Cols that have built-in and custom CSS applied.
1. Why are some components that are rendered within the HeaderForm Component also have various styling frameworks (and potentially CSS) applied to them.
1. Why aren't there constraints to the width of the input elements, such as tighter column spacing, or direct CSS application impacting their size?
1. TBD

There is more work to do here, and this is a work in progress.

### General Hierarchy

The React App Components in this project are as follows from Parent, through all children:

```text
App
 |
HeaderForm
  |
DataPositionFormRow
| | | |
| | | PathNameFormRow
| | |
| | BedRegionsFormRow
| |
| FileUploadFormRow
|                  |
MountedDataFormRow |
|                  |
[ SelectionDropdown ]
```

*Note* that the grandchild Component is utilized by 2 different parent components.

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

*Note*: If you haven't built since the last change, your changes might not take effect!

## Footer

Return to [Root README](../README.html)
