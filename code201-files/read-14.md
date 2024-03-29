# Notes from Various Readings

[What Google Learned About Teams](#what-google-learned-from-its-quest-to-buid-the-perfect-team)  
[CSS Transforms](#css-transforms-article-notes)  
[Transitions and Animations](#transitions-and-animations)  

## What Google Learned from its Quest to Buid the Perfect Team

In the age of information, data, and cubicles, it turns out that collaborative efforts and activities has increased a lot in the last few decades.  
But just being "on a team" is not always enough to get beneficial effects.  
Some benefits of working with others as a pair or team of 3 or more are:

- Improvements in innovation. As a group multiple minds come up with more ideas to work with.  
- Improvements in quality work. Mistakes are found more quickly with extra sets of eyes.  
- The social aspect: Being social tends to help while bouncing ideas off of each other and talking through things that otherwise could not be talked through.  

Teamwork might not be good enough, on its own.  
*How* team members work together is important.  

Google created a project, "Aristotle", to research why some teams were very effective while others struggled.  

- No true "stick these types of people together and they will perform" tactic seemed to be any more effective than other tactics.  
- Research data did not indicate trends in the makeup of teams vs their effectiveness or how well they got along.  

### Group Norms

"Norms are the traditions, behavioral standards and unwritten rules that govern how we function when we gather..." *[NYT Magazine (Duhigg, Charles)]*

These play a part in how a group acts and feels, and maybe how 'attractive' a group might be for some people, but it still does not define how productive or 'efficient' the group is.  

### Collective IQ

Teams that succeed tend to succeed a lot; teams that fail tend to continue failing.  
Group 'norms' played a part in teams' effectiveness and ability to succeed.  

### Conversational Turn Taking

Teams where everyone had roughly the same amount of time to speak generally performed better than others where few members dominated most conversations.  
The Collective IQ of a team that shared speaking time evenly tended to be higher.  

### Silent Communications

Teams where members were aware of how other members were feeling and what their needs were tended to perform better. The example provided was reading people's body language, and allowing a conversation to take a turn, allowing that person to talk-out what they wanted to say, thereby actively participating in the group.  

### Psychological Safety

Without a safe-space to speak, some people simply won't speak, which ends up negatively impacting the entire team.  
The fear of punishment or reprise for speaking up is enough to keep some people from doing so.  
People are more likely to "be themselves" if they are in a safe place, and trust those around them.  
One person interviewed for the article said emotional conversations are related to psychological safety.  

### Where to Go From Here?

When a team leaves you feeling exhausted, it is unlikely to be an efficient or successful team.  
For the Aristotle project, the question of how to raise developers social awareness of interpersonal queues, when (generally speaking) they just want to work with computers and code, and not so much their feelings.  
Mr. Laurent said "...I had separated things in my head into work life and life life. But the thing is, my work is my life. I spend the majority of my time working. Most of my friends I know through work. If I can't be open and honeset at work, then I'm not really living, am I?" *[Laurent, a Google employee, interviewed by NYT Magazine (Duhigg, Charles)]*.

## Jon's Key Takeaways

Be yourself.  
Be open with your employer and your team mates.  
Remember to be empathetic and to allow time for others to talk and contribute.  
Help to maintain a safe space for social interactions, to make for better interactions and teamwork.  
Since work is a significant part of life, embrace your team as part of your life -- as a family of sorts.  

[New York Times Magazine](https://www.nytimes.com/2016/02/28/magazine/what-google-learned-from-its-quest-to-build-the-perfect-team.html)  

## CSS Transforms Article Notes

[ShayHowe.com css transforms](https://learn.shayhowe.com/advanced-html-css/css-transforms/)

Transforms change html elements including size and position.  
The `transform` property does *not* enjoy great browser support, so using vendor prefixes to fend against problems is strongly recommended.  

```css
.element-class {
/* vendor prefixes */
-webkit-transform: ...;
-moz-transform: ...;
-o-transform: ...;
transform: ...;  /* native, overwrites others if supported */  
}
```

### 2D Transforms

Think of transform meaning 'to distort'.  
2D transforms operate on x- and y- axes.  
3D transforms operate on 2D plus the z- plane.  
The origin of a transform is the center of the element.  
*Note*: Think of xyz and length, width, depth.  

#### Rotate

Rotates an element by n degree units from -360 to 360.  

```css
div {
  transform: rotate(-100deg); 
}
```

#### Scale

Size: transform: scale(0.01 to >1.01)
Horizontal Size: transform: scaleX(n)  
Vertical Size: transform: scaleY(n)  

#### Translation

Does not interrupt the normal flow of the document.  
Pulls an element away from its normal position.  
Same syntax as transform ( translate() translateX() translateY() ).  
Use px or percentage units.  

#### 2D Skew

Distort elements on X-, Y-, or both Axes.  
Use to transform a box or rectangle into a polygon or rhomboid.  
Syntax similar to Scale.  
Units are in degrees.  

*Note*: This CAN NOT be used on 3D transforms - it must be achieved using other 3D transform properties.  

#### Combining Transforms

In the Transform: statement include the types of transforms and their settings, in-line, without commas.

```css
section {
 transform: rotate(150deg) scale(1.25);
}
```

#### Transform Origin

The basis or center-point upon which a transform is based can be moved using 'transform-origin'.  
Units can be px or percentages.  
Single-argument: X- and Y- planes.
Double-argument: (xPlane yPlane).  

#### Perspective Property

The "vanishing point".  
Apply to the parent element OR as a second property setting in the transform property setting.  
Set units in px.  

#### Perspective Depth

Units can be `none` or a length measurement.  
Tilts the object using x- or y- plane.  

#### Perspective Origin

Values and units used in transform-origin can be used here.  
Determines the vanishing point location.  

### 3D Transforms

3-dimensional transforms incorporate the Z-axis.  

#### 3D Rotate

Changes elements along the Z axis in addition to X and Y.  
Transform can take `perspective()` and `rotate` settings.  
`rotateX()`, `rotateY()`, `rotateZ()`.  
Rotate units are 'deg'.

```css
#boxone {
  transform: perspective(150px) rotateX(25deg);
}
#boxtwo {
  transform: perspective(100px) rotateZ(150deg);
}
```

#### 3D Scale

Scale the box on its Z-axis.  
Use with rotate or another transform to see its effect.  

```css
#boxthree {
  transform: perspective(100px) scaleZ(1.80) rotateY(230deg);
}
```

#### 3D Translate

Translate on the Z-axis.  
Effectively shrinks and expands an elements i.e.: closer or further away, at the viewer's perspective.  
Units are in px.  

```css
#boxfour {
  transform: perspective(100px) translateZ(-20);
}
```

#### 3D Skew

Cannot be done - use other transform properties to meet the desired effect.  

#### 3D Transform Shorthand

Rotate3d, Scale3d, Transition3D, and Matrix3D support CSS Shorthand.  
Experiment first, it is complicated.  

### Transform Style

Use to manage transformations applied to nested elements.  
Allows maintaining 3d space properly when trnasforms are applied to a parent element, and then its child.  

```css
.childelement {
  transform-style: 
}
```

### Backface Visibility

Causes a fully rotated element to no longer be visible until rotated back.  

```css
.alpha {
  transform: rotateY(180deg);
}
.bravo {
  backface-visibility: hidden;
  transform: rotateY(180deg);
}
```

### References

ShayHowe.com has multiple links at the bottom of the article with more resources on these topics.

[ShayHowe.com css transforms](https://learn.shayhowe.com/advanced-html-css/css-transforms/)

## Transitions and Animations

Transition and animation effects can be accomplished with little added code in CSS3. When your website pops, it is more interesting, and attracts attention.  

### Transitions in General

- Alter element behavior and appearance.
- Hover, focus, active, and target.
  - 'target' matches a string in the selection portion of the current URL.  
- Animations are accomplished via 'keyframes'.  
- Transitions change an elements state.  
- Animations need transition points on different keyframes to get the intended effect.  

#### Transitions

Changes the state of an element. In the first example the .box class selector sets the following properties:  

- background
- transition-property
- transition-duraction
- transition-timing-function

Then the pseudo-class `:hover` is used to apply a different background for when the element is *not* hovered.  

#### Vendor Prefixes

In order to accomplish some compatibility, especially with newer CSS3 properties and older browsers, vendor prefixes are used:  

- `-webkit-*`: Android, Chrome, iOS, Safari browsers  
- `-moz-*`: Firefox browser  
- `-ms-*`: Microsoft (i.e. IE)  
- `-o-*`: Opera browser  

Follow vendor prefixes with the CSS property.  
Each line could include a vendor-prefixed property.  
The property on its own should be last in the list of properties (after vendor-prefixed ones).  

### Transitional Property  

Determines which properties will be altered: `transitional-property: property;`  
Follow that with `transition-duration: #s;` and `transition-timing-function: [linear | ];`  

*Note*: Not all properties may be transitioned! Only properties that have a clear set of "in between values", such as `color:`  

### Transition Duration

Set in seconds as integers or decimal, e.g. '.2s'.  
Set one for each transition property.  
Multiple transition-property properties will use a single `transition-duration:` if it is the only one declared.  

### Transition Timing

Assigns a speed of movement calculation type to the transitioning property.  

- linear
- ease-in
- ease-out
- ease-in-out

Timing functions use a cubic-bezier curve to calculate timings.  
Additional control over each timing function is possible:  

- `cubic-bezier(x1, y1, x2, y2);`
- `setp-start;`
- `step-stop;`
- `steps(number-of-steps, direction);`

### Transition Delay

A delay can be added using the property `transition-delay:`.  
Values can be s or 0.s (seconds or milliseconts) of 'stalling time'.  

### Shorthand Transitions

Like many other CSS3 properties, a shorthand version is available.  
The order is:  

```css
div {
  transition: {transition-property transition-duration transition-timing-function transition-delay};
}
```

*Note*: Only use commas when targeting *multiple transitions*.  

### More Examples

See [this article](https://learn.shayhowe.com/advanced-html-css/transitions-animations/) for transition examples like a cool button click and a card-flip transition.  

## Animations

Many of the same concepts that apply to transitions also apply to animations.  

- Property `keyframes:` `@keyframes name { n { properties }};`  
- Vendor prefixes  

Animations have additional properties:

- `animation-name: slide;`: Defines which keyframe rule to apply to.
- Follow animatin-name with animation-duration with a value.  

### Animation Duration Timing Function and Delay

Animations that call on an animation name share properties with transitions.

- `animation-duration: seconds;`  
- `animation-timing-function: function;`  
- `animation-delay: seconds;`  

### Customizing Animations

Additional setings of animations include the number of times an animation runs and the direction it completes.  

- `animation-iteration-count: infinite | count;`  
- `animation-direction: normal | reverse | alternate | alternate-reverse;`  
- `animation-play-state: running | paused;`
- `animation-fill-mode: none | forward | backward | both;`  

### Shorthand Animations

Like many other CSS3 properties, a shorthand version is available.  
The order is:  

```css
div {
  animation: {animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-direction animation-fill-mode animation-play-state};
}
```

### Additional Resources

See the collection of links at the end of the Animation section.

## Eight Simple CSS3 Transitions

[Web Designer Depot article](https://www.webdesignerdepot.com/2014/05/8-simple-css3-transitions-that-will-wow-your-users)  

Sarah Vieira writes, in a 2014 article, about hardware accelerated css rules that will help improve website design and interest, with very few lines of code. This is a general overview highlighting key points.

1. Do the usual html layout and use IDs or Classes to target filters to specific elements.
2. Set a height, width, background and us the transition property `transition: all 0.3s ease;`
3. Leverage pseudo elements to adjust the opacity property, e.g. div and div:hover `opacity:0.5;` and `opacity:1.0;`  
4. Animate a color change by altering the background property on e.g. div:hover `background: some_other_color;`  
5. Use 'Transform' to grow and shrink elements e.g. `.grow:hover { -webkit-transform: scale(1.3); -ms-transform: scale(1.3); transform: scale(1.3); }`  
6. To shrink, use transform the same as in 5, above, using values less than 1.0.  
7. RotateZ will add a rotation animation e.g. `.rotate:hover { transform: rotateZ(90deg);}`  
8. Use border-radius to transform a square into a circle: `.circle:hover { transform: border-radius: 50%; }`  
9. Adding a shadow to a box is good, but 3D is better right? `.three-d-shadow:hover { box-shadow: 1px 1px #color, 2px 2px #color, 3px 3px #color; }`  
10. Add a 'shiver' animation by defining `@keyframes`and `transform: translateX()`, then apply it e.g. `swing.hover { animation: swing 1s ease; animation-iteration-count: 1;}`  
11. Use 'inset border animation'. Rather than just add a border that can change the size and location of the element, apply box-shadow e.g.: `.border:hover { box-shadow: inset 0 0 0 25px #color; }`  

*Note*: Remember to include back-level browser properties e.g. `-webkit-transform`, `-ms-transform`, etc.  

### Fade In

Create two CSS3 rules that target the specific element to fade and apply a `:hover` pseudo element to one of them:

```css
.fade {
  opacity: 0.5;
}
.fade:hover {
  opacity:1;
}

### Change Color

```css
.color:hover {
  background:#53a7ea;
}
```

### Grow and Shrink

```css
.grow:hover {
  -webkit-transform: scale(1.3);
  -ms-transform: scale(1.3);
  transform: scale(1.3);
}
.shrink:hover {
  -webkit-transform: scale(0.8);
  -ms-transform: scale(0.8);
  transform: scale(0.8);
}
```

### Rotate Elements

```css
.rotate:hover{
  -webkit-transform: rotateZ(-30deg);
  -ms-transform: rotateZ(-30deg);
  transform: rotateZ(-30deg);
}
```

### Square to Circle

```css
.circle:active{
  -webkit-animation: swing 0.5s ease;
  animation: swing 0/5s ease;
  -webkit-animation-iteration-count: 1;
  animation-iteration-count: 1;
}
.circle:hover{
  border-radius:50%;
}
```

### 3D Shadow

```css
.threed:hover{
  box-shadow: 1px 1px #53a7ea,
    2px 2px #53a7ea,
    3px 3px #53a7ea;
  -webkit-transform: translateX(-3px);
  transform: translateX(-3px);
}
```

### Swing

```css
.swing:hover
{
  -webkit-animation: swing 1s ease;
  animation: swing 1s ease;
  -webkit-animation-iteration-count: 1;
  animation-iteration-count: 1;
}
```

### Inset Border

```css
.border:hover{
  box-shadow: inset 0 0 0 10px #53a7ea;
}
```

### Combining

Recall that multiple CSS3 selectors can be added to a class attribute in a space-separated list.

```html
<div class="border circle">Inset Border</div>
```

When the element renders, CSS3 rules from BOTH class selectors will apply:

- When pointed at (hover) both rules, names 'border' and 'circle' apply.
- When cursor is *not* over the elements, neither 'border' nor 'circle' selectors take effect.

```css
.border:hover{
  box-shadow: inset 0 0 0 10px #53a7ea;
}
.circle:hover{
  border-radius:50%;
}
```

This way the page can leverage both CSS selectors independantly, perhaps pointing to other similar elements that should only render one effect or the other.

[ShayHow.com css transitions and animations](https://learn.shayhowe.com/advanced-html-css/transitions-animations/)

## Three Buttons Animated

This links to a codepen.io environment similar to replit.com, and displays the HTML and CSS3 necessary to animate 3 buttons that move up and down. Pseudo-class 'hover' has CSS3 rules that stop the up-and-down translation animation, stopping the buttons motions.

## CSS3 Keyframes

This is a codepen.io demonstration using keyframes to animate a ball (a child div) with `position: absolute;` set, inside of a box (parent div).
Both divs are set with inline styles that set the animation to keyframes by name ('bouncing').
The properties set in the keyframe definition sets timing, starting and animated relative locations (in px) to create the illusion of movement.  

Keyframe Animation in [codepen.io](https://codepen.io/akshaychauhan/pen/dyBqVo) *[akshaychauhan, codepen.io animation designer]*  

## 404 Animation

Another codepen.io demonstration animates the number 404 using multiple keyframes.  

Keyframe Animation in [codepen.io](https://codepen.io/kieranfivestars/pen/MYdQxX) *[Kieran Hunter]*  

## Pure CSS Bounce Animation

CSS as an artform 101: [codepen.io](https://codepen.io/dp_lewis/pen/QWMxRR)_ *[David Lewis]*  

## Back to Readme

[Back to index in readme](./README.md)
