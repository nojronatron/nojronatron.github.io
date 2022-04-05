# ES 6 Classes Lecture Notes

## Data Modeling

Use constructor functions and prototypes to model data.  
ES6 Classes will help.  

### Classes

Classes have attributes and behaviors.  

- Attributes describe what something *is*.  
- Behaviors describe what something *does* or *can do*.  
- Inheritance can help with templating many types of similar instances.  

### Constructor Function Syntax and Use

ES6 sytax and best practices for creating Constructor Functions:

- Use `const` to define a Constructor Function.  
- Use Pascal case to name Classes and Constructor Functions.  
- Prototype Function names are all lower-case.  
- Prototype Functions allows adding new Attributes and Behaviors to an existing instance.  
- Properties can be set by invokation of methods on an instance of a Class.  
- By adding a Constructor Class Method, a lot of memory is used. Instead, use Prototype Functions.  
- By adding a Prototype Function, it is not stored *with* the Class or Constructor Method instance, saving memory. Rather, it is just associated with every instance of the class.  
- Create a Prototype Function that mirrors the 'parent' object but it associated with the *child* object instance.  
- InstanceOf: `instance InstanceOf type` will output Boolean if Instance template is teh same.  

#### Key Takeaways

- Cumbersome syntax.  
- 'Heavy' code, with lots of duplicate or similar code.  

ES6 Classes make this easier.  

### New Way Using EF5 Classes

Use keyword `class` to define a Class specifically.  
Pascal-case the class name.  
Constructor Function used to initialize the Class instance.  
Functions (with and without parameter lists) are bolted-on simply.  

An example directly from the *[CodeFellows Lecture on EF6 Classes]*:

```javascript
class Animal {
  constructor(name, legs) {
    this.name = name;
    this.legs = legs;
  }
  walk() {
    this.isWalking = true;
  }
  eat() {
    this.isEating = true;
  }
}
```

#### Prototype Methods Are Automatic

When using Classes, Prototype Methods are *automatic*.  
In the previous example, `walk()` and `eat()` are actually Prototype Methods.  

#### Keyword Extends

The 'extends' keyword tells JS to use the Class that follows as its 'parent' or 'base' class.  
The newly created Class automatically acquires the attributes and behaviors of the 'extended class'.  

```javascript
class Dog extends Animal {

}
let rosie = ne Dog('Rolph', 4);
rosie.walk();
rosie.eat();
console.log(rosie);
```

#### Parents and Inheritance

Extends does lots of work for you by 'inheriting' the attributes and behaviors of the 'parent class'.  
Extends creates a 'child class'.  
