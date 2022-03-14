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
