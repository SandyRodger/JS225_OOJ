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

  - What is meant by 'Implicit function execution context'?
    - When a function is called its context is saved in an object referenced by the `this` variable. If a context is not explicitly set using apply, bind, or call, then Javascript implicitly sets the context. This is what is meant by `implicit function execution context`. Its an important concept in Javascript because context depends on how the function is called, rather than where it is defined. These work by rules that are completely different to variable scoping rules. Let's look at a few examples:

```javascript
let obj = {
  a: 1,
  foo: function() {
    console.log(this.a)
  }
}

obj.foo() // 1
// In the example above we have the Object dot function pattern where javascript automatically sets the method's context to the object it is called on.
let bar = obj.foo
bar() // undefined
// In this example above we are demonstrating context loss where a function is saved to a variable, but the references to its variables is lost. bar() is called on the top-level, so `this` is set to the global object. As there is no `a` variable defined on the global object the function prints `undefined`.
```
    - If we wanted to prevent context loss we could ensure that our functions operate with explicit function execution context, by using apply, bind or call or an arrow function.

  - What is meant by 'explicit function execution context'?
    -  Continuing from the previous answer, one can bind a function's context explicitly with apply bind or call, or with an arrow function. These are excellent ways to avoid context loss. They are demonstrated below:

```javascript
let obj = {
  a: 1,
  foo: function(num1, num2, num3) {
    console.log(`${this.a} and ${num1}, ${num2}, ${num3}`)
  }
}

//apply
obj.foo.apply(obj, [12, 13, 14])
//call
obj.foo.call(obj, 1, 2, 3)
//bind
let boundFoo = obj.foo.bind(obj)
boundFoo(4, 5, 6)
//arrow function:
let obj2 = {
  a: 1,
  foo: function(n1, n2, n3) {
    let bar = () => { console.log(`${this.a} and ${num1}, ${num2}, ${num3}`) }
    bar(n1, n2, n3)
  }
}
obj.foo(7, 8, 9)
```

  - What is context loss and how does one deal with it?
  - Explain lexical scope
scope and closures:
  - What are higher order functions?
  - How does one create and use private data?
  - What is garbage collection?
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
Weak-points:
  - What are closures?
    - When a function is defined Javascript saves a reference to the variables in scope at time of definition (but only if the function needs them). This means that when the function is invoked later at a different point in the program it "remembers" these variables. So closures are a combination of a function and its lexical environment. Closures are saved in memory, so a developer does not have access to them. Closures allow devs to implement private data/behaviour, partial function application and function factories . Closures persist until a function is no longer accessible (and therefore eligible for "garbage collection").
  - Arrow functions:
1.  In callback functions
let obj = {
 a: 'hello',
 b: 'world',
 foo() {
    [1, 2, 3].forEach((number) => {
 console.log(String(number) + ' ' + this.a + ' ' + this.b);
    });
  },
};

obj.foo();
// => 1 hello world
// => 2 hello world
// => 3 hello world
2.  In nested functions inside methods:
let obj = {
 a: 'hello',
 b: 'world',
 foo: function() {
 // Traditional function would lose context
 let bar = () => {
 console.log(this.a + ' ' + this.b);
    }
 
 bar(); // => hello world
  }
};

obj.foo();

3.  When functions are passed as arguments


Remember:

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
