# Notes from Duckett HTML and JS Books

Notes taken from Ducketts JavaScript and JQuery book while skimming Chapters 3 and 5.

## Chapter 3: Objects (pg.100)

### Introduction

- JS Objects model things, and data.  
- Properties describe what things are, and store data in variables.  
- Functions defined in an Object are known as 'Methods' and are what the Object *can* do.  
- Properties are `key:value` pairs: Property name is the Key, and the property value is the Value.  
- Methods are  also `key:value` pairs: Method name is the Key, the Function definition is the value.  
- Key-Value pairs can hold any JavaScript type: Array; String; Number; etc.  

### Literal Notation

Create an object using *Literal Notation* *[Duckett, pg.102]*  

```javascript
var hotel = {
  name: 'Quay',
  rooms: 40,
  booked: 25,
  checkAvailability: function() {
    return this.rooms - this.booked;
  }
}
```

### Accessing An Object

After creating a new object, access the object properties using dot notation:  

```javascript
let totalRooms = hotel.rooms;
```

Do the same to access Methods:  

```javascript
let currentAvailableRooms = hotel.checkAvailability();
```

The dot is known as a *member operator*.  

Property access is also allowed through *square bracket syntax*, but not Methods:  

```javascript
let bookedRooms = hotel[rooms];
```

Objects can also be created using *Constructor Notation*:  

```javascript
let car = new Object();
car.color = "blue";
car.speed = 0;
car.model = "civic";
car.speedUp = function() {
  this.speed++;
};
```

*Note*: Using Constructor notation to add or remove objects only impacts the named instantiated object.

Property values can also be *updated* using Square Bracket Notation:

```javascript
hotel[rooms] = 52;
```

### Templating Object Creation

1. Create a function that has arguments representing the object properties.  
2. Use *Literal Notation* to assign the arguments to properties, and define the object method(s).  
3. Assign the template to a new Pascal-case variable using the *new* keyword and supply the necessary argument values.
4. The resulting variable will be the new object.  

```javascript
//  using literal notation to assign arg to props
function Hotel (name, rooms, booked) {
  this.name: 'Quay';
  this.rooms: 40;
  this.booked: 25;
  this.checkAvailability: function() {
    return this.rooms - this.booked;
  };
}

//  using the object template to create new instance
let snoqualmieHotel = new Hotel("Snoqualmie Falls Lodge", 20, 11);
let tulalipHotel = new Hotel("Tulalip Hotel", 235, 287);
```

### Adding and Removing Properties

Add properties by using the following notation:  

```javascript
snoqualmieHotel.className = 'address' = "123 Summit Lane, Snoqualmie, WA";
```

Remove properties by using the 'delete' keyword:  

```javascript
delete snoqualmieHotel.address;
```

### Keyword 'this'

- Always refers to a single object, in which a function operates.  
- Specifies the parent object as the target of the referenced property or method.  
- Keyword is always bound by the object it is contained within, or 'global' if at the root level of the code page.  

### About Objects

- Used to store data e.g.: Hotels, Arrays, etc.  
- Arrays can contain objects in their elements.  
- Objects can contain Arrays as their data.  
- Use 'dot notation' to access object Properties.  
- Use object Properties to store child objects.  

There are three primary types of objects:

1. Browser Object Model: Has many child objects, properties, and other members.  
2. Document Object Model: Each element is stored in an object, and attributes are stored as object properties.  
3. Global Javascript Objects: String; Number; Boolean; Date; Math; Regex; etc.  

### Object Model Members

Browser Object Model:

Duckett Pg.124 has a listing of Browser Object Model properties and methods.

Document Object Model:

Duckett Pg.126 has a listing of Document Object Model properties and methods.  

*Note*: If you use a member, like Alert(), and do not specify the model, Browser object will be called by default.

### Global JS Objects

Duckett Pgs.128,129 has a large table of many String properties and how to use them.  

### Working With Data Types

Primitive Data Types:

- String  
- Number  
- Boolean  
- Undefined (does not have an Object)  
- Null (does not have an Object)  

Complex Data Types:

- Object: Includes Arrays and Functions (callable/executable objects).  

## Chapter 5: Docment Object Model (pg.183)

Overview:

- The Document Object Model (DOM) Tree is represented by the web browser.  
- Document nodes, Element nodes, Attribute nodes, and Text nodes are part of the DOM Tree.  
- ID and CLASS attributes are used to select nodes. CSS Selector Syntax can be used.  
- NodeList represents the resulting list of Nodes when the DOM Tree is queried.  
- Using DOM manipulation techniques, or textContent and innerHTML properties, element nodes can be read from and written to.  
- Element Node nesting is common as are siblings of Text Nodes and other child Elements.  
- Again, browser support of the DOM Tree varies, especially back-level version support (this is where JQuery comes in handy).  
- The DOM Tree can be viewed using tools buit-in the modern web browsers.  

### DOM Tree

Think of this like an 'Org Chart' of a web page.  

- Document Node: The Parent node at the top-of-the-document level, containing all other elements and objects.  
- Element Nodes: Include items like Inline and Block-level Elements.  
- Attribute Nodes: Contain attributes stored in opening elements in HTML.  
- Text Ndoes: Store text *within an Element Node*.  

Recall that all object will have their own set of Properties and Methods.  

#### Working With The DOM Tree

You must select an Element Node before gaining access to the other Node types:  

1. Using single-select techniques: getElementById() or querySelector()  
2. Using select-multiple techniques: getElementsByClassNam(), getElementsByTagName(), or querySelectorAll()  
3. Using Tree Traversal: parentNode, previousSibling, nextSibling, firstChild, lastChild  

Once selected, elements can be manipulated:

1. Text is stored in Text Nodes. Access it through firstChild property and then nodeValue to get the value.  
2. Access Text Nodes through innerHTML and textContent.  
2a. Create content: createElement(), createTextNode(), appendChild()  
2b. Remove content: removeChild()  
3. Attributes are accessed and updated via hasAttribute(), getAttribute(), setAttribute(), and removeAttribute()  

*Note*: Text Node is a dead-end leaf. To get to child-element text, access must be made through the parent node(s).  

Use variables to store elements and values that will be used more than once.  

```javscript
let fooElement = getElementById('foo');
```

#### Accessing Elements

A DOM Query will return a collection of results, even if only one element was found.  
Use bracket (index) syntax to access the disired element.  
Always use the "fastest route" to the element you seek, to keep the UI responsive and appear "fast".  

DOM Query Getters that return a single element:

- getElementById('id');
- querySelector('css selector');

DOM Query Getters that return a NodeList:  

- getElementByClassNma('class');  
- getElementsByTagNam('tagname');  
- querySelectorAll('css selector');

*Note*: Again, browser support will vary, but `document.getElementById('id');` is recommended (been around the longest).  

#### Live and Static Node Lists

Using `getElementsBy...` is quicker and automatically updates your stored nodeLists.  
Using `querySelector...` is slower and stored nodeLists are *not* udpated automatically.  

Live: Select one or multiple elements using `getElementsByTagName('tagName');`, `getElementsByClassName('className');`.  
Static: Select all elements at a level in the DOM using `querySelectorAll('element[id]');`.  

*Note*: Elements returned by dynamic DOM Queries appear in the collection in the same order they appear in the DOM Tree.  

#### Elements Within a NodeList

The item() method: Returns individual node within a NodeList, similar to Indexing but uses parentheses instead of brackets.  
Using array syntax: Index into the NodeList using square brackets.  

#### Looping Through a NodeList

Repeat the same action on every Node in a NodeList using Looping structures.  

### Traversing the DOM

Walk the tree through element types using the following properties:  

- `parentNode`: The Node that *contains* the currently selected Node.  
- `previousSibling` and `nextSibling`: The next or previous Node that shares the exact same Parent Node.  
- `firstChild` and `lastChild`: The first or last child node to the currently selected Node.  

### Whitespace Nodes

Most browsers count whitespace as individual Nodes, sibling to other text, inline, or block level nodes.  

### Access and Update Text Using NodeValue

From *[Duckett, pg.214]*:  

```javascript
document.getEleemntById('one').firstChild.nextSibling.nodeValue;
```

1. The 'li' element is selected using getElemntById().  
2. First Child of `<li>` is the `<em>` element.  
3. The text node is the *next sibling* of that `<em>` element.  
4. (...) access contents using nodeValue.  

*Key Takeaway*: Use 'nodeValue' to access and update text in nodes, either within a selector or through custom variables.  

### Adding and Removing HTML Content

The DOM allows adding and removing Nodes.
Use 'innerHTML' property to do this.
Can be used on any Element Node to ADD or REPLACE content.  
String content can include descendant element HTML markup.  

Adding Content Process *[Duckett, pg.218]*:

1. Store new content (including markup) as a string in a variable.  
2. Select the element whose content you wnat to replace.  
3. Set the element's innerHTML property to be the new string.  

Remove Content Process *[Duckett, pg.218]*, depending on the type:  

- Set innerHTML to an empty string.  
- Remove single element from DOM fragment: Provide the entire fragment minus that element.  

To put changes to the DOM Tree, use separate methods to prepare-and-set the Node(s), one at a time:

1. Capture or create Node content.  
2. Attach a Node to the correct spot in the DOM Tree.  

For Removal, just use a single method, separate from the add and edit methods.  

Get/Set Examples:

```javascript
var foo = document.getElementById('bar').innerHTML; //  GETs the HTML from element ID 'bar'
document.getEleementById('doh').innerHtml = foo;      //  SET element with ID 'doh' with value of variable 'foo'
```

### Adding Elements Using DOM Manipulation

Process overview:  

1. Create and store a new element node with `createElement()` method into a new variable.  
2. 