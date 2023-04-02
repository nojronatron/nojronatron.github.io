# Breaking Down Code Problems

Presenter: Monika Davies

Topic: Breaking down problems in javascript

This is an important web development skill.

Demo app will be to build Rock-paper-scissors, an HTML, CSS, and JavaScript single-page app.

## Necessary Steps To Get Started

Get requirements:

- Players: How many? How few?
- Moves: What is the move order, steps, and requirements or limitations?
- Conditions of game end: Win, lose, draw, etc.

Consider UI Structure:

- User interface, overall.
- Header and/or Hero image with title.
- Buttons.
- Section for game messages.
- Section for a score.

Consider Styling:

- Static CSS.
- Animations.
- Colors.
- Fonts.
- Element positioning.

Consider Functionality and Dynamic Aspects:

- Handlers that respond to events.
- Functions that accepts input.
- Display selections on-screen.
- Make announcements as appropriate.
- Tally statistics.
- Allow starting a new game.

Consider Artifacts:

- Needed background or header images.
- Button and icon files.

## Other Tidbits

Input type elements aren't that much different than Button elements, and can be set written to handle events like a button would.

Use ID's to enable elements that can display data and have it get dynamically updated e.g. Player Score.

Find all items with class name 'class' and store them in a variable: `const buttons = document.querySelectAll('.class')`

Add an event listener with `button.addEventListener('click', handlerFunction)`

Use Console.Log to verify event listeners are working.

Need to select an item randomly from a string array? Use Random, but put its bounds between 0 and max index of the array, then use array indexing to get the item from the array with the random index number.

Is there a large matrix of possible outcomes:

- Could write a long list of if statements. Long, ugly, difficult to maintain.
- Consolidate if statements into _outcomes_ to eliminate many options. e.g. a Tie is `Player.selection === Computer.selection` which handles 3 possible conditions in one.
- Use logical OR to consolidate multiple possible outcomes into a single if statement.
- Remaining statement must be the remaining combinations that haven't been matched.

## Footer

Back to [PPH Index](./pph-index.html)

Return to [Root README](../README.html)
