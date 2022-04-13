# Read02 Assignment - State And Props

Read and take notes from the following resources:

ReactJS [Lists and Keys](https://reactjs.org/docs/lists-and-keys.html)  
The Spread Operator on [Medium.com](https://medium.com/coding-at-dawn/how-to-use-the-spread-operator-in-javascript-b9e4a8b06fab)  

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

Scenario:

- Parent Component rendered a collection of child components.  
- Each child component has an event handler that needs to set or change State in the parent component.  

To Do:

1. Create and register an event handler function in the child Component whose State is to be changed.  
2. Create an event handler function in the Parent that will update the this.state.stateName of the Child component that called it, by using the replacement technique (so React can detect the State change and re-render automatically).  
3. In the Parent component, pass-in a prop and assign it the value of the Parent's event handler function (created in step 2, above) i.e. `handler={this.stateChngFuncName}`  
4. In the Child component, call the method that was passed-in at step 3 and pass-in any rqeuired parameters i.e. `this.props.stateChngFuncName(this.props.name);`.  


## Other Reference Links

React [Tutorial](https://reactjs.org/tutorial/tutorial.html)  
React [Lifting UP State](https://reactjs.org/docs/lifting-state-up.html)  

## Footer

Go back to [Readme.md](../README.html)  
