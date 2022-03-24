# Notes from Various Readings

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

"Norms are the traditions, behavioral standards and unwritten rules that govern how we function when we gather..." *[]*

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

https://learn.shayhowe.com/advanced-html-css/css-transforms/

## CSS Transforms Article Notes

Transforms change html elements including size and position.  
The `transform` property does *not* enjoy great browser support, so using vendor prefixes to fend against problems is strongly recommended.  

```css
/* vendor prefixes */
-webkit-transform: ...;
-moz-transform: ...;
-o-transform: ...;
transform: ...;  /* native, overwrites others if supported */  
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

Changes elements along the Z axis in addition to X and Y.  



## Back to Readme.md

[Back to index in readme](./README.md)