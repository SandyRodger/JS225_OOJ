# Assessment Prep

- Take assessment: Monday 21st April (12 days) Or earlier? Next Tuesday?
  - Now Tuesday 22nd -> I lost focus. New Target Tuesday 29th?
  - Assessment format changes May 2nd (in 10 days).
- Then another study guide and a practice project
- Take home project for which you have 24 hours.

### Schedule

- JS229 assessment Easter Monday (21st April)
- JS230/239 -> May
- TS240/249 -> 1/2 June
- Re-do RB119 -> 2/2 June
- Prep capstone -> July
- Move out -> beginning of July

### to do
  - Finish JS225 exercises (twice?)
  - Finish JS210 exercises where I can't find that I've done them (twice?)
  - Read:
    - JavaScript Weekly: Understanding Links on the Object Prototype Chain
    - JavaScript Weekly: An Introduction to First-Class Functions
    - JavaScript Weekly: What in the World is this?!

### done

  - Study your LS181 assessment where you got 100%. This is the technique to use.
  - create comprehensive document (js_225 readme) which has my notes + hyper-links to the parts of the course that reference the relevant material.
    - Read these articles
      - JavaScript Weekly: Making Sense of Closures (read 8.4.25)
    - Create calendar that fits Srdjan's suggested time-frame
    - Read discussion board for JS229
    - Write a list of expected questions with answers
    - Cancel AM's wedding

### to maintain

- Continually be adding to Anki deck
- Maintain art. I think It's necessary for my equilibrium. Specifically daily drawings + tutorials
- Be ruthless about getting excellent sleep. (no alcohol) \:

### to mull

- Start working afternoons?
- How am I going to use LSbot to prepare for this exam?

## [Assessment Format:](https://launchschool.com/lessons/d6ad18da/assignments/b39fe5b1)

- 2 parts:
  1) A 3 hour written test (aproximately 20 questions)
  2) A take-home project -> Apply the concepts in code.

## [Part 1: Study Guide for the Test](https://launchschool.com/lessons/d6ad18da/assignments/588f2f82)

- You need to be able to explain and apply the following concepts:
  - Objects:
    - Organising code into the appropriate objects
    - Object factories
  - Determining/setting function execution context (this)
    - Implicit function execution context
    - explicit function execution context
    - dealing with context loss
    - lexical scope
  - scope and closures
    - higher order functions
    - creating and using private data
    - garbage collection
    - IIFEs
    - Partial function application
  - Object creation patterns
    - class syntax
    - constructor functions
    - pseudo-classical pattern
    - Prototype objects
    - Behaviour delegation.  

## My mock assessment:
  - What are higher order functions?
  - How does one create and use private data?
 - What are IIFEs and why would one use them?
  - What is Partial function application? (Why is it used?, what is it good for? How is it executed?)
Object creation patterns
  - What are the different object creation patterns covered in this course?
  - How does one write a class in Javascript? (class syntax)
    - Inheritance?
    - Polymorphism?
  - How are constructor functions used in javascript?
  - What is the pseudo-classical pattern?
  - Prototype objects
    - What are function prototypes?
      -  Every non-arrow-function function in Javascript has a property called 'function prototype' that points to its function prototype.
      -  The function prototype is an object.
      -  In this object there is a constructor property, which actually points back to the function itself.
      -  When the function is used with the `new` keyword to create an object, the newly created instance has a `[[prototype]]` property which points to the contructors prototype property.
  - Behaviour delegation.

## LSbot quiz

Function Prototype Practice Questions

1.  ​Basic​: What is the difference between a function's prototype property and an object's internal [[Prototype]] property?

A function's prototype property and an object's [[Prototype]] property serve different but related purposes:
•   ​Function's prototype property​:
   •   This is a regular, accessible property that exists on constructor functions
   •   It references an object that will become the prototype for instances created when the function is called with new
   •   It contains shared properties and methods that all instances created from this constructor will inherit
   •   It automatically contains a constructor property that points back to the function
•   ​Object's [[Prototype]] property​:
   •   This is an internal, hidden property of objects (accessed via Object.getPrototypeOf())
   •   It references the object from which properties are inherited (the next object in the prototype chain)
   •   When a constructor creates an object with new, the object's [[Prototype]] is set to the constructor's prototype object
   •   When a property is accessed on an object but not found, JavaScript follows this link to look up the prototype chain

2.  ​Intermediate​: What will the following code output and why?
<!---->
// javascript

   function Dog(name) {
     this.name = name;
   }
   
   Dog.prototype.bark = function() {
     return `${this.name} says woof!`;
   };
   
   let fido = new Dog('Fido');
   Dog.prototype.bark = function() {
     return `${this.name} says WOOF WOOF!`;
   };
   
   console.log(fido.bark()); 

   - 'Fido says WOOF WOOF!' (I got it wrong first time)

3.  ​Intermediate​: Explain the purpose of the following code and what pattern it demonstrates:
<!---->
// javascript

   function Dog(name, breed, weight) {
     this.name = name;
     this.breed = breed;
     this.weight = weight;
   }
   
   Dog.prototype.bark = function() {
     console.log(this.weight > 20 ? 'Woof!' : 'Yip!');
   };
   
   let maxi = new Dog('Maxi', 'German Shepherd', 32);

  -  This code is written in classical Prototypal inheritance pattern and shows how we can use prototypal inheritance to create objects

4.  ​Advanced​: Write code to implement the following functionality:
<!---->
// javascript

   let foo = {
     a: 1,
   };
   
   let bar = foo.begetObject();
   foo.isPrototypeOf(bar);         // true

Answer:

```

let foo = {
  a: 1,
};

Object.prototype.begetObject = function() {
  return Object.create(this);
};

let bar = foo.begetObject();
let r = foo.isPrototypeOf(bar);
console.log(r)
```
