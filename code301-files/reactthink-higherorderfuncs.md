# Readings for 15Apr2022

[Thinking in react](https://reactjs.org/docs/thinking-in-react.html)

## Start With A Mock

Mock-up of what a site page looks like.
An example of JSON data that the page will consume, i.e. from an API.

## Break Up The UI

Think of the UI as a Component hierarchy.  

1. The entire mocked-up page.  
2. Header or top-of-page component(s).  
3. An output area or main body of the page, which could be thought of as a table.  
4. Row headings.  
5. Possibly iterable row content.  

## Build a Static React Site

Start with the main page that handles the UI layout but has no interactivity.  
Add Components that reuse other components and pass props but *do not use state* in this version.  
Start building top-down or bottom-up, whatever your preference.  

You should end up with a number of components that are used to render the data in the main page.  

### ID the Minimal Representation of UI State

### ID Where State Should Be

### Add Inverse Data Flow

### Interesting Notes

Building the static portion of the website will require lots of typing but not much thinking.
Building the interactivity of the website will require lots of thinking and not much typing.  

## Thinking In React Q and A

What is the single responsibility principle and how does it apply to components?
What does it mean to build a ‘static’ version of your application?
Once you have a static application, what do you need to add?
What are the three questions you can ask to determine if something is state?
How can you identify where state needs to live?

[Higher Order Functions](https://eloquentjavascript.net/05_higher_order.html#h_xxCc98lOBK)  

What is a “higher-order function”?
Explore the greaterThan function as defined in the reading. In your own words, what is line 2 of this function doing?
Explain how either map or reduce operates, with regards to higher-order functions.

## Footer

Go back to [Readme.md](../README.html)  
