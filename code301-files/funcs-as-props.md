# Read02 Assignment - State And Props

Read and take notes from the following resources:

ReactJS [Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)  
The Spread Operator on [Medium.com](https://medium.com/coding-at-dawn/how-to-use-the-spread-operator-in-javascript-b9e4a8b06fab)  
Steve Griffith YouTube Channel [Episode 22 Passing Functions between Components](https://www.youtube.com/watch?v=c05OL7XbwXU)  
React Tuturial through [Declaring a Winner](https://reactjs.org/tutorial/tutorial.html)  
Lifting State from [Reactjs documentation](https://reactjs.org/docs/lifting-state-up.html)  

## Lists and Keys

What does .map() return?

> A new array of elements resulting from the callback function.  

If I want to loop through an array and display each value in JSX, how do I do that in React?

> Use a map function and a callback function like: `(item) => { <div>{item}</div> }`  

Full code example:

```javascript
function NumList(props) {
  const nums = props.nums;
  const liItems = nums.map((num) =>
    <ListItem key={num.toString()}
              value={num} />
  );
  return (
    <ul>
      {liItems}
    </ul>
  );
}
```

Each list item needs a unique ____.

> KEY  

What is the purpose of a key?

> React uses Keys to track when items have changed.  

See also [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)  

## The Spread Operator

What is the spread operator?

> It is a  string of characters: '...'  

List 4 things that the spread operator can do.

1. It is used to expand an array into individual elements.  
2. Copy and array.  
3. Concatenate / combine arrays.  
4. Adding a state in React.  

Give an example of using the spread operator to combine two arrays.

> `[...[1, 2, 3], ...[4, 5, 6]] === [1, 2, 3, 4, 5, 6]`  

Give an example of using the spread operator to add a new item to an array.

> `[[4],...[1,2,3,]] === [4, 1, 2, 3]`  

Give an example of using the spread operator to combine two objects into one.

> `{ ...{title: "one"}, ...{title: "two"}, color: () => {"red"} }`  

*Note*: Copying an array or object with the spread operator creates a copy with new references, so changing the original will *not* change the spread-copied array values. => "SHALLOW COPY"  

## Pass Functions Between Components

Ref [link](https://www.youtube.com/watch?v=c05OL7XbwXU)  

### Scenario

- Parent Component rendered a collection of child components.  
- Each child component has an event handler that needs to set or change State in the parent component.  

### How To Do It

1. Create and register an event handler function in the child Component whose State is to be changed.  
2. Create an event handler function in the Parent that will update the this.state.stateName of the Child component that called it, by using the replacement technique (so React can detect the State change and re-render automatically).  
3. In the Parent component, pass-in a prop and assign it the value of the Parent's event handler function (created in step 2, above) i.e. `handler={this.stateChngFuncName}`  
4. In the Child component, call the method that was passed-in at step 3 and pass-in any rqeuired parameters i.e. `this.props.stateChngFuncName(this.props.name);`.  

### Q and A

In the video, what is the first step that the developer does to pass functions between components?

> Prior-to, the dev created and registers an event handler function in the child component whose State is to be changed.  
> Next, the dev created a function in the Parent that will update the this.state.stateName of the Child Compoennt that called it, and implemented the replacement technique so React will automatically re-render.

In your own words, what does the increment function do?

> There are two increment functions:
> The Parent one: It matches the people 'state' object by their name property, the increments that instance property 'count' by 1.  
> The Child one: Sets the state property 'hasChanged' to true, and calls the Parent's 'increment()' function, and passes-in the Components this.props.name.  

How can you pass a method from a parent component into a child component?

> Add a property to the Component Instantiation of the Parent components Render method, so that each Child component instantiation is provided with the 'increment' property referencing the Parent components 'increment()' method.  

How does the child component invoke a method that was passed to it from a parent component?

> The Child componoent calls the method passed-in using this syntax: `this.props.funcName(this.props.propertyName);`.  

## Lifting State


## Other Reference Links

React [Tutorial](https://reactjs.org/tutorial/tutorial.html)  
React [Lifting UP State](https://reactjs.org/docs/lifting-state-up.html)  

## Footer

Go back to [Readme.md](../README.html)  
