# Object Oriented javascript

## [Introduction](https://launchschool.com/books/oo_javascript/read/introduction)
### [Why JavaScript?](https://launchschool.com/books/oo_javascript/read/introduction#whyjavascript)
- It's ubiquitous (front and back end)
- Javaascript implements OOP with prototypes rather than classes like most other languages
### What is Object-Oriented Programming?
### Who is this Book For?
## [Types and Objects](https://launchschool.com/books/oo_javascript/read/types_and_objects)
- sounds a lot like RB120
### [Objects](https://launchschool.com/books/oo_javascript/read/types_and_objects#objects)
  - type v class:
    - type usually refers to a primitive object
    - Class refers to an object defined with the `class` keyword
  - objects are sometimes called instances or instance objects and are often created by a constructor function

```javascript
function Cat(name) {
  this.name = name;
}

let butterscotch = new Cat("Butterscotch");
let pudding = new Cat("Pudding");
```
- here calling the `cat` function with the `new` keyword makes it a constructor function.

### [Classes and Types](https://launchschool.com/books/oo_javascript/read/types_and_objects#classestypes)
-  Confusion
### [Creating Objects](https://launchschool.com/books/oo_javascript/read/types_and_objects#creatingobjects)
- You can create functions inside Object classes so instances are created with the behaviour to manipulate its data.
- When object properties have functons we call them methods
### [Concise Method Syntax](https://launchschool.com/books/oo_javascript/read/types_and_objects#concisemethodsyntax)

- covered before
### [The `this` Keyword](https://launchschool.com/books/oo_javascript/read/types_and_objects#this)
```javascript
let student = {
  name: 'Joanna',
  age: 27,

  study() {
    console.log(`${this.name} is studying`);
  },

  pass() {
    console.log(`${this.name} has passed this course`)
  },
};

student.study();  // Joanna is studying
student.pass();   // Joanna has passed this course
```
- `this` is apparently a source of much confusion. I'm not sure why as it appears to do the same job as `.self` in Ruby
### [State and Behavior](https://launchschool.com/books/oo_javascript/read/types_and_objects#statebehavior)
- This is all familiar from RB 120

### [Summary](https://launchschool.com/books/oo_javascript/read/types_and_objects#summary)

- yup

### [Exercises](https://launchschool.com/books/oo_javascript/read/types_and_objects)

1. 
```javascript
let Cessna152Aircraft = {
  fuelCapacity: 24.5,
  cruisingSpeedInKnots: 111,
  takeOff() {
    console.log('I am taking off');
  },
  land() {
    console.log('I am landing');
  }
}
```
  - fuelCapacity and cruisingSpeedInKnots are states, the 2 functions are behaviours.
2.
```javascript
function Book(title, author, year) {         // this is the constructor function
  this.title = title,
  this.author = author,
  this.yearPublished = year
}

let neuromancer = new book('Neuromancer', 'William Gibson', '1984')     // these are the object instance, their type is 'object' - apparently this is incorrect. Their object type is Book even though calling typeof with them will return 'object'
let doomsdayBook = new book('Doomsday Book', 'Connie Willis', '1992')
```

3. 

```javascript
**// this is the constructor function
function Album(title, artist, released) { 
  this.title = title,
  this.artist = artist,
  this.released = released
}

// these are the instance objects
let thriller = new Album('Thriller', 'Michael Jackson', 1982); // type = Album, 
let darkSide = new Album('The Dark Side of the Moon', 'Pink Floyd', 1973);
```
4. 
```javascript
function SmartPhone(brand, model, releaseYear) {
  
  this.brand = brand,
  this.model = model,
  this.releaseYear = releaseYear

  this.checkBattery = function() {
    return `${this.brand}, ${this.model} has 75% battery remaining`
  }
  this.displayInfo = function() {
    return `${this.brand}, ${this.model} was released in ${releaseYear}`;
  }
}

let phone1 = new SmartPhone('Apple',	'iPhone 12',	2020)
let phone2 = new SmartPhone('Samsung',	'Galaxy S21',	2021)

console.log(phone1.checkBattery());
console.log(phone2.displayInfo());
```

## [The Object Model](https://launchschool.com/books/oo_javascript/read/the_object_model)
### [Encapsulation](https://launchschool.com/books/oo_javascript/read/the_object_model#encapsulation)
### [Polymorphism](https://launchschool.com/books/oo_javascript/read/the_object_model#polymorphism)

### [Inheritance](https://launchschool.com/books/oo_javascript/read/the_object_model#inheritance)


### [Summary](https://launchschool.com/books/oo_javascript/read/the_object_model#summary)
### [Exercises](https://launchschool.com/books/oo_javascript/read/the_object_model#exercises)

1. polymorphism
2. Inheritance - wrong -> encapsulation
3.  make, model, year, -> state | methods that provide the ability to start, drive, and park the vehicle -> behaviour.
4.  Inheritance

## [Object Factories](https://launchschool.com/books/oo_javascript/read/object_factories)

### [What is an Object Factory?](https://launchschool.com/books/oo_javascript/read/object_factories#whatisanobjectfactory)

- we've covered this already

### [Advantages and Disadvantages of Object Factories](https://launchschool.com/books/oo_javascript/read/object_factories#advantagesdisadvantages)

- Advantages
  - s let programmers create highly customized objects
  - a more straightforward way to create objects without dealing with the complexities of prototype chains
  -  bypass one of the trickiest JavaScript concepts you will encounter: execution context and the associated this keyword
- Disadvantages
  - Each object created by a factory function gets copies of the methods defined by the returned object.: factory functions can use high amounts of memory when creating many objects.
  -  can be more cumbersome and less performance-efficient than the more advanced approaches
  -   the objects they create don't have a "type"

### [When Should You Use Factory Functions?](https://launchschool.com/books/oo_javascript/read/object_factories#whentousefactories)

When you do not need inheritance.
When your application already uses object factories.
When you aren't concerned about memory usage or only expect to use a small number of objects.
When you only have a few simple types in your code. In such cases, you're unlikely to have problems if you need to inspect objects while debugging.
When the specific type of an object is unimportant to your application.

#### But avoid in these circumstances:

When inheritance is required.
When you need many objects with methods.
When the types of your objects are essential to your application.

### [Summary](https://launchschool.com/books/oo_javascript/read/object_factories#summary)
### [Exercises](https://launchschool.com/books/oo_javascript/read/object_factories#exercises)

1.

```javascript
function makeFruit(name, color) {
  return {
    name,
    color,
    isRipe: function() {
      return `This ${this.name} is ripe.`;
    },
  
    describe: function() {
      return `This ${this.name} is ${this.color}.`;
    },
  }
}

let apple = makeFruit('apple', 'red');
let banana = makeFruit('banana', 'yellow');
let blackberry = makeFruit('blackberry', 'purple');
console.log(blackberry.describe());
```

2.

```javascript
function makeSmartPhone(brand, model, releaseYear) {
  return { 
    brand,
    model,
    releaseYear,
    checkBattery() {
      return `${this.brand}, ${this.model} has 75% battery remaining`
    },
    displayInfo() {
      return `${this.brand}, ${this.model} was released in ${releaseYear}`;
    }
  }
}

let phone1 = new makeSmartPhone('Apple',	'iPhone 12',	2020)
let phone2 = new makeSmartPhone('Samsung',	'Galaxy S21',	2021)

console.log(phone1.checkBattery());
console.log(phone2.displayInfo());
```
 
## [Classes](https://launchschool.com/books/oo_javascript/read/classes)
### [Defining Classes](https://launchschool.com/books/oo_javascript/read/classes#definingclasses)


### [Class Inheritance](https://launchschool.com/books/oo_javascript/read/classes#classinheritance)

#### Inheritance Hierarchies

### [When Should You Use ES6 Classes?](https://launchschool.com/books/oo_javascript/read/classes#whentouseclasses)


### [Summary](https://launchschool.com/books/oo_javascript/read/classes#summary)
### [Exercises](https://launchschool.com/books/oo_javascript/read/classes#exercises)

1. 
```javascript
/*

Write a class that can be used to instantiate objects that represent smartphones. Each smartphone should have a brand, model, and release year. Add methods to check the battery level and to display the smartphone's information. Create objects that represent the following 2 smartphones:


*/

class SmartPhone {
  constructor(brand, model, year) {
    this.brand = brand,
    this.model = model,
    this.year = year,
    this.battery = 50,
    this.info = 'It\'s a phone';
  };
  checkBattery = function() {
    console.log(`battery is on ${this.battery}%`)
  };
  displayInfo = function() {
    console.log(`Status: ${this.info}`)
  }
}

let p1 = new SmartPhone('Apple',	'iPhone 12',	'2020');
let p2 = new SmartPhone('Samsung',	'Galaxy S21',	'2021');
p1.checkBattery();
p2.displayInfo();
```

2. `instanceof`

3.

```javascript
/*
Create a class hierarchy consisting of vehicles, including cars, boats, and planes, as specific kinds of vehicles. All vehicles should be able to accelerate and decelerate. Cars should be able to honk, boats should be able to drop anchor, and planes should be able to take off and land. Test your code.

All vehicles should have a color and weight. Cars have a license number, boats have a home port, and planes have an airline name.
*/

class Vehicle {
  constructor(colour, weight) {
    this.colour = colour;
    this.weight = weight;
  }
  accelerate = function() {
    console.log(`I have accelerated`);
  }
  decelerate = function() {
    console.log('I have decelerated');
  }
}

class Car extends Vehicle {
  constructor(colour, weight, license) {
    super(colour, weight);
    this.license = license;
  }
  honk = function() {
    console.log('Toot toot!')
  }
}

class Boat extends Vehicle {
  constructor(colour, weight, homePort) {
    super(colour, weight);
    this.homePort = homePort;
  }
  dropAnchor = function() {
    console.log('Splosh!')
  }
}

class Plane extends Vehicle {
  constructor(colour, weight, airline) {
    super(colour, weight);
    this.airline = airline;
  }
  takeOff = function() {
    console.log('Up up and away')
  };
  land = function() {
    console.log('Ladies and gentlemen we\'ve arrived at our destination')
  }
}

let plane = new Plane('pink', '2000', 'WhizzAir')
plane.accelerate()
console.log(plane)
let car = new Car('black', '1000', 'R816 KPN');
car.honk();
let boat = new Boat('blue', '30000', 'Brest');
boat.accelerate()
```

```javascript
let plane = new Plane('pink', '2000', 'WhizzAir')
let car = new Car('black', '1000', 'R816 KPN');
let boat = new Boat('blue', '30000', 'Brest');
console.log(car instanceof Vehicle)
console.log(car instanceof Car)
console.log(boat instanceof Vehicle)
console.log(!(boat instanceof Car))
```

## [More About Classes](https://launchschool.com/books/oo_javascript/read/more_classes)

### [Private Fields and Methods](https://launchschool.com/books/oo_javascript/read/more_classes#privatefieldsmethods)

```javascript
class Foo {
  #data;
  #initializedData = 43;
  constructor(value) {
    this.#data = value;
  }

  show(){
    console.log(this.#data, this.#initializedData);
  }
}

let foo = new Foo(42);
foo.show();
```

### [Getters and Setters](https://launchschool.com/books/oo_javascript/read/more_classes#getterssetters)

Getters:

```javascript
class Student {
  constructor(firstName, lastName, track) {
    this._firstName = firstName;
    this._lastName = lastName;
    this._track = track;
  }

  get name(){
    return [this.firstName, this.lastName]; 
  }

  get firstName() {
    return this._firstName;
  }

  get lastName() {
    return this._lastName;
  }

  get track() {
    return this._track;
  }
}

let student = new Student('Sandy', 'Rodger', 'Ruby');
console.log(`${student.name.join(' ')} ${student.track}`);
console.log(`${student.firstName} ${student.lastName}`);
```

Setters:

```javascript
let teacher = {
  firstName: 'Alan',
  lastName: 'Stone',

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  set name(nameArray) {
    this.firstName = nameArray[0]
    this.lastName = nameArray[1]
  },
};

teacher.name = ['Snadweh', 'Bicycle-feet']
console.log(teacher.fullName);
```

### [Static Fields and Methods](https://launchschool.com/books/oo_javascript/read/more_classes#staticfieldsmethods)

-  So are these like class methods/class objects in Ruby ?

### [Summary](https://launchschool.com/books/oo_javascript/read/more_classes#summary)

- Urgh there's a lot (I suspect I would learn this better by doing).

- Ordinary **object properties** are known by several synonymous terms:
  -  instance properties,
  -  public fields
  -  public class fields. Instance properties belong to a class's instance objects. By default, they are public. Any user of an object can access or update the values of those properties.

- Likewise, ordinary **object methods** are variously known as:
  - instance methods,
  - public methods,
  - public class methods. Instance methods belong to instance objects and are, by default, public. Any user of an object can call those methods.

- **Private fields** are known by several synonymous terms:
  - private properties,
  - private instance properties,
  - private class fields. Private fields belong to a class's instance objects but are private: only the methods inside the class can access them. Private fields are named with a leading # and must be declared before they can be used.

- Likewise, **private methods** are variously known as:
  - private instance methods
  -  private class methods. Private methods belong to a class's instance objects but are private: they can only be called by the instance methods defined by the class. Private methods are named with a leading #.

- **Static fields** are variously known as:
  -  static properties
  -  class properties. They are, by default, public and belong to the class, not instances of the class. You must use the class name or a reference to the class to access static fields; you can't use an instance object.

- **Static methods** are sometimes called:
  -  class methods. They are, by default, public and belong to the class, not instances of the class. You must use the class name or a reference to the class to call the method; you can't use an instance object.

### [Exercises](https://launchschool.com/books/oo_javascript/read/more_classes#exercises)

1.
```javascript
class Person{
  #name;
  #age;

  constructor(name, age) {
    this.#name = name;
    this.age = age;
  }

  set age(age) {
    if (typeof(age) === 'number' && age > 0) {
      this.#age = age;
    } else {
      throw new RangeError('Age must be positive');
    }
  }

  showAge() {
    console.log(this.#age);
  }
}

let person = new Person('John', 30);
person.showAge()
```

2.
```javascript
/*

Create a Book class with private fields title, author, and year. Provide getters for each field and a setter for the year field that raises a RangeError if year is before 1900.

*/

class Book {
  #title;
  #author;
  #year;

  constructor(title, author, year) {
    this.#title = title;
    this.#author = author;
    this.year = year;
  }

  get title() {return this.#title };
  get author() {return this.#author };
  get year() {return this.#year };

  set year(newYear) {
    if (newYear < 1900) {
      throw new RangeError('Invalid year');
     } else {
      this.#year = newYear;
    }
  }
}

let book = new Book('The Great Gatsby', 'F. Scott Fitzgerald', 1925);
console.log(book.title);  // The Great Gatsby
console.log(book.author); // F. Scott Fitzgerald
console.log(book.year);   // 1925

book.year = 1932;         // Changing year
console.log(book.year);   // 1932

try {
  book.year = 1825;
} catch (e) {
  console.log(e);   // RangeError: Invalid year
}

try {
  let book2 = new Book('A Tale of Two Cities', 'Charles Dickens', 1859);
} catch (e) {
  console.log(e);   // RangeError: Invalid year
}
```

3. 

## [Prototypal Inheritance](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance)

- A core Javascript feature.
- Yes we know that objects can inherit behaviours and properties from classes, but they can also inherit them from other objects and that's what this chapeter is about.
- Most other OO languages have a classical inheritance model. Not this one baby! Javascript is weird.
- Prototype objects can contain properties, but most of them only contain methods, so this chapter will ignore prototype's containing ordinary properties.
- Most javascript devs use classes in new code. This chapter is important because we need to understand how classes work behind the scenes with the prototype system.gma
- 

### [Prototype Objects](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#prototypeobjects)

- Rememeber properties can be defined on objects without being stored in the prototype. The prototype is how objects inherit from other objects. if you define a function on an object it's not affected by this stuff.
- 2 types (related, but different):
  - function prototypes
  - object prototypes

#### My fantasy model for prototypes:

- This is a fantasy world where we have creatures born of a queen (class), who roam around with external amniotic sacs protruding from their bellies (prototypes). In the sacs are scrolls (data) and deamons (functions). The god of this world is Javascript.
- The creatures are called `Objakts`.
- When God wants to create a Queen Objakt (class) it conjures a special type of deamon called a "Konz-trak-Tah" ('Constructor'). This deamon makes a magic bag full of lesser deamons (functions) and sews that onto the Queen (class) (saved to the prototype property). This sac is called the function prototype.
- Each queen Objakt contains its own mini-constructor deamon, which its own creator "Konz-trak-Tah" made as an act of vanity inside its creation.
- When god creates an Objakt from the Queen he looks at the queen's amneiotic sac and clones it in the new baby.
- Weirdly each sac is itself an independent species of Objakt, a sort of parasitical dwarf-species, and each of these has it's own sac. Where the Objakt's sac is the same as its parent, this sub-sac is identical to the Objakt's grandparent.

##### World schema:
  - God -> Javascript
  - Queen Objakts -> classes
  - Deamons -> functions
  - Scrolls -> data
  - drone Objakts -> Objects
  - amneiotic sacs -> properties
  - main amneiotic sac -> prototype property.

### Function prototypes:

- Most functions and classes have a property called `prototype` which stores the function prototype.
  -  When we create a class (`Cat` for example) javascript invisibly creates a "constructor" function for that class (not the same as the constructor method you have included).
  -  This constructor creates an object (called the function prototype) which contains the methods you've written in your class.
  -  The object is than saved as a `prototype` property of the `Cat` class.
    - recap:
       - I write a class.
       - Javascript behind the scenes make a function ("constructor")
       - the constructor makes an object ("function prototype") containing the methods in your class
       - the function prototype is saved as a property of the class.

### Object Prototypes:

- All javascript objects have an object prototype. This is an object containing all of methods the an object inherits. like the function prototype - so is prototype just another word for "bag of methods"?)
- `Object.getPrototypeOf(*instance object name*);` returns the object prototype.
- With almost all objects you can follow the chain of prototypes up the an object called `Object.prototype`. This is called the **prototype chain**.
- The prototype of `Object.prototype`is null. So every prototype ends with null.

#### When Objects Inherit Directly From Object:

- yeah-obviosuly. You make an object, it is an Objakt spawned from its queen, `Object` and so has the same function prototype, wich we've just learnt is `null`, so ut ain't inherited shit.

#### Accessing Object Prototypes

- You can't access the prototype directly, only via the `getPrototypeOf` method.

#### Reassigning Object Prototypes:

- `Object.setPrototypeOf`

#### Object Prototypes for Functions and Classes

#### Arrow Functions and Function Prototypes

#### The __proto__ Property

- dunder
- Deprecated

#### Accessing Function Prototypes

- 

### [The Prototype Chain](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#theprototypechain)

- "class keyword is syntactic sugar that maps to a constructor function and a function prototype." -> isn't all code syntactical sugar, in the sense that it hides layers of more complex language that the computer use using?
  - LS response:
  - You're right that in a broad sense, most programming constructs could be considered "syntactic sugar" for lower-level operations. However, in programming terminology, "syntactic sugar" has a more specific meaning.
When we say the class keyword in JavaScript is syntactic sugar, we mean it doesn't introduce any new capabilities to the language - it's just a more convenient way to write code that uses the existing constructor functions and prototypes. As shown in the JS225 materials, the class syntax directly maps to the pseudo-classical pattern that was already possible:
// javascript

// This class syntax
class Point {
  constructor(x = 0, y = 0) {
    this.x = x;
    this.y = y;
  }
  
  onXAxis() {
    return this.y === 0;
  }
}

// Is equivalent to this constructor function syntax
function Point(x=0, y=0) {
  this.x = x;
  this.y = y;
};

Point.prototype.onXAxis = function() {
  return this.y === 0;
};
The key distinction is that syntactic sugar offers an alternative syntax for something that was already possible in the language, without changing the underlying mechanics or adding new capabilities. It just makes certain patterns more convenient to express.
In contrast, many language features aren't considered syntactic sugar because they introduce fundamentally new capabilities or concepts that weren't previously expressible.
JavaScript's class syntax was specifically added to make the language more approachable to developers coming from class-based languages like Java or Ruby, even though JavaScript's object system remains prototype-based under the hood.

### [Constructor/Prototype Pattern](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#constructorprototypepattern)
  - 2 more typos:
    - OOJS book -> Prototypal Inheritance -> Constructor/Prototype Pattern -> 2nd code snippet -> line 10 -> "we meed to simulate super()"
    - OOJS book -> Prototypal Inheritance -> Constructor/Prototype Pattern -> 2nd paragraph -> "(for now, we'll ignore the inheritance aspect of this code for now)"
### [When Should You Use the Constructor/Prototype Pattern?](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#whentouseconstructorprototype)
### [Summary](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#summary)
### [Exercises](https://launchschool.com/books/oo_javascript/read/prototypal_inheritance#exercises)

1. 

```
function Phone(brand, model, releaseYear) {
  this.model = model;
  this.brand = brand;
  this.releaseYear = releaseYear;
  this.batteryLevel = 75;
}

Phone.prototype.information = function() {
  console.log(`This phone is a ${this.brand} ${this.model} released ${this.releaseYear}`)
}

Phone.prototype.battery = function() {
  console.log(`Battery level is ${this.batteryLevel}%`)
}

let phoneA = new Phone('Apple',	'iPhone 12',	'2020');
let phoneB = new Phone('Samsung',	'Galaxy S21',	'2021');
phoneA.information()
phoneA.battery()
phoneB.information()
phoneB.battery()
```

2.

```javascript
/*

This exercise re-examines exercise 3 from the previous chapter. In that exercise, you wrote a class hierarchy to represent vehicles of various types. In this exercise, we'll rewrite that solution using the constructor/prototype pattern.

Using the constructor/prototype pattern, create some types that represent vehicles, including cars, boats, and planes as specific kinds of vehicles. All vehicles should be able to accelerate and decelerate. Cars should be able to honk, boats should be able to drop anchor, and planes should be able to take off and land. Test your code.
*/

function Vehicle(name) {
  this.name = name;
}

function Car(name) {
  Vehicle.call(this, name);
}

Car.prototype = Object.create(Vehicle.prototype);
Car.prototype.constructor = Car;
Car.prototype.honk = function() {
  console.log(`My ${this.name} honks.`);
};

function Boat(name) {
  Vehicle.call(this, name);
}

Boat.prototype = Object.create(Vehicle.prototype);
Boat.prototype.constructor = Boat;
Boat.prototype.dropAnchor = function() {
  console.log(`My ${this.name} drops anchor.`);
};

function Plane(name) {
  Vehicle.call(this, name);
}

Plane.prototype = Object.create(Vehicle.prototype);
Plane.prototype.constructor = Plane;
Plane.prototype.takeOff = function() {
  console.log(`My ${this.name} takes off.`);
};
Plane.prototype.land = function() {
  console.log(`My ${this.name} lands.`);
};

let myCar = new Car('volvo');
myCar.honk()

let myBoat = new Boat('yacht');
myBoat.dropAnchor()

let myPlane = new Plane('jet');
myPlane.takeOff()
```
## My Progress

First read: March 2025
Second Read: April 2025 (5th - )


# [JS225_OOJ](https://launchschool.com/courses/a920bdfc/home)

## 1 About this Course
### What this course covers
  - Dig deeper into Javascript:
    - functions
    - Execution context
    - scope
    - closures
    - OOJ
  - After this course you will be able to:
    - build basic applications in Javascript
    - Move on to the next course, in which you will:
      - create more complex Javascript projects that:
        - Interact with the DOM
        - Have more user interactivity
## [2 Objects](https://launchschool.com/lessons/4671d66f/home)

### [1	Introduction](https://launchschool.com/lessons/4671d66f/assignments/d4d78556)
  - Objects -> the most versatile of Javascript's data types
  - There's a lot to learn, even relative to the other lessons. Buckle up.

### [2	Prerequisites](https://launchschool.com/lessons/4671d66f/assignments/41ceaaeb)
  - Concise property & concise method syntax.
  -  instead of this:
```javascript
function foo(bar) {
  return {
    bar: bar,
    qux: function() {
      console.log("hello");
    },
  };
}
```
  -  We can do this:
```javascript
function foo(bar) {
  return {
    bar,                      // same as bar: bar
    qux() {                   // same as qux: function()
      console.log("hello");
    },
  };
}
```

### [3	Begin the Object-Oriented JavaScript Book](https://launchschool.com/lessons/4671d66f/assignments/bba44185)

- For now just read:
  - Introduction
  - types and objects

### [4	Objects and Methods](https://launchschool.com/lessons/4671d66f/assignments/42efa5b4)

#### Function and method invocation

```javascript
let greeter = {
  morning: function() {
    console.log('Good morning!');
  },
};

function evening() {
  console.log('Good evening!');
}

// Method invocation
greeter.morning();   // greeter is the receiver/calling object; morning() is a method

// Function invocation
evening();           // there is no explicit receiver; evening() is a function
```

- You can see that the morning method must be called via its class.
  - `  morning: function() {`
- Whereas the evening function is merely stored inside this class and so can be called without reference to it.
  - `function evening() {`

#### `this` during method invocation

- seems pretty straight-forward
```javascript
let counter = {
  count: 0,
  advance: function() {
    this.count += 1;
  },
};

counter;                // { count: 0, advance: [Function] }

counter.advance();
counter;                // { count: 1, advance: [Function] }

counter.advance();
counter.advance();

counter;                // { count: 3, advance: [Function] }
```


### [5	Walkthrough: Object Methods](https://launchschool.com/lessons/4671d66f/assignments/cd3f4b07)

```javscript
let me = {
  firstName: 'Sandy',
  surname: 'Rodger',
}

let friend = {
  firstName: 'Connie',
  surname: 'Chadwick',
}

let mum = {
  firstName: 'Susan',
  surname: 'Rodger',
}
function introduce(person) {
  console.log(`Here is ${person.firstName} ${person.surname}.`)
}

let people = [];
people.push(me);
people.push(friend);
people.push(mum);

function rollCall(people) {
  people.forEach(introduce)
}

rollCall(people)
```

OR

```javascript
let me = {
  firstName: 'Sandy',
  surname: 'Rodger',
}

let friend = {
  firstName: 'Connie',
  surname: 'Chadwick',
}

let mum = {
  firstName: 'Susan',
  surname: 'Rodger',
}

let people = {
  collection: [me, friend, mum],
  introduce: function(person) {
    console.log(`Here is ${person.firstName} ${person.surname}.`)
  },
  rollCall: function() {
    this.collection.forEach(this.introduce);
  },  
};

people.rollCall()
```
AND FINALLY:
```javascript
let people = {
  collection: [],
  nextAvailableID: 400,
  introduce: function(person) {
    console.log(`Here is ${person.firstName} ${person.surname}. ID ${person.id}`)
  },
  rollCall: function() {
    this.collection.forEach(this.introduce);
  },  
  add: function(person) {
    if (this.isInvalidPerson(person)) return;
    person.id = this.nextAvailableID;
    this.collection.push(person);
    this.nextAvailableID++;
  },
  getIndex: function(person) {
    let index = -1;
    this.collection.forEach(function(comparator, i) {
      if (comparator.firstName === person.firstName &&
          comparator.surname === person.surname) {
          index = i;
        }
    })
    return index;
  },
  remove: function(person) {
    let index = this.getIndex(person);
    if (!this.isInvalidPerson(person)) return;
    if (index === -1) return ;
    this.collection.splice(index, 1);
  },
  isInvalidPerson: function(person) {
    return typeof person.firstName !== 'string' ||
           typeof person.surname !== 'string';
  },
  get: function(person) {
    if (this.isInvalidPerson(person)) return false;
    return this.collection[this.getIndex(person)];
  },
  update: function(person) {
    if (this.isInvalidPerson(person)) return;
    let existingPersonID = this.getIndex(person);
    if (existingPersonID === -1) {
      this.add(person);
    } else {
      this.collection[existingPersonID] = person;
    }
  }
};

class Person {
  constructor(firstName, surname) {
    this.firstName = firstName;
    this.surname = surname;
  }
}
let me = new Person('Sandy', 'Rodger');
let friend = new Person('Connie', 'Chadwick');
let mum = new Person('Susan', 'Rodger');

// people.rollCall();
// console.log(`--------------`)
people.add(me);
people.add(friend);
people.add(mum);
// console.log(`--------------`)
people.rollCall();
```

### [6	Practice Problems: Objects](https://launchschool.com/lessons/4671d66f/assignments/90e3243c)

```javascript
class item {
  constructor(name, amount) {
    this.name = name;
    this.amount = amount;
  }
}
let invoices = {
  unpaid: [],
  paid: [],
  payInvoice: function(clientName) {
    for (i = 0; i < this.unpaid.length; i++) {
      if (this.unpaid[i].name === clientName) {
        this.paid.push(...this.unpaid.splice(i, 1))
      }
    }
  },
  add: function(clientName, amount) {
    if (typeof clientName !== 'string' || typeof amount !== 'number') return;
    this.unpaid.push(new item(clientName, amount));
  },
  totalDue: function() {
    let total = this.unpaid.reduce((acc, obj) => obj.amount + acc, 0);
    console.log(total);
  },
  totalPaid: function() {
    let total = this.paid.reduce((acc, obj) => obj.amount + acc, 0);
    console.log(total);
  }
}



// invoices.add('Barry', 1);
// invoices.add('Melanie', 2)
// invoices.add('Walter', 3);
invoices.add('Due North Development', 250);
invoices.add('Moonbeam Interactive', 187.50)
invoices.add('Slough Digital', 300);
invoices.payInvoice('Due North Development')
invoices.payInvoice('Slough Digital')
invoices.totalPaid();
invoices.totalDue();
``` 

### [7	Mutating Objects](https://launchschool.com/lessons/4671d66f/assignments/35a7fec7)

- all familiar
- Watch [this](https://www.youtube.com/watch?v=9ooYYRLdg_g) when Youtube is not blocked 

### 8	Practice Problems: Mutating Objects

1. (correct)
Hello from the function scope!
Hello from the global scope!
2. Correct (demonstrates the mutability of obejcts)
'Greetings from the function scope!'
'Greetings from the function scope!'
3. Incorrect
```javascript
let message = 'Hello from the global scope!';

function func() {
  message = 'Hello from the function scope!';
  console.log(message);
}

func();
console.log(message);let message = 'Hello from the global scope!';

function func() {
  message = 'Hello from the function scope!';
  console.log(message);
}

func();
console.log(message);
```
- In this example we don't pass `message` into the function, so it finds the variable in the global scope and that is where it is reassigned.
4.
false
true
5.
Because we reassign the `animal` variable to a different object.

### [9	Collaborator Objects](https://launchschool.com/lessons/4671d66f/assignments/a0e5532d)

- Storing objects in other objects. Like theres a `pet` class and and `person` class. You can store a pet object in the person object to say the person owns the pet.
- Collaborators needn't be custom objects. Technically strings and almost everything is really a collaborator because these objects are more complicated than they seem.

### [10	Functions as Object Factories](https://launchschool.com/lessons/4671d66f/assignments/6463ca43)

```javascript
function makeCar(acceleration, brakeRate) {
  return {
    speed: 0,
    rate: acceleration,
    brakeRate: brakeRate,
    accelerate() {
      this.speed += this.rate;
    },
    brake() {
      if (this.speed >= this.brakeRate) {
        this.speed -= this.brakeRate;
      } else {
       this.speed = 0;
      }
    },
    printSpeed() {
      console.log(this.speed);
    }
  };
}

let sedan = makeCar(8, 6);
sedan.accelerate();
sedan.printSpeed(); // 8
sedan.brake();
sedan.printSpeed() // 2
sedan.brake();
sedan.printSpeed() // 0
let coupe = makeCar(12, 6);
coupe.accelerate();
// console.log(coupe.speed); // 12
let hatchback = makeCar(9, 6);
```

- There are other ways to create objects. This way is the object factory. 

### [11	Practice Problems: Functions as Object Factories](https://launchschool.com/lessons/4671d66f/assignments/e45ab60c)

```javascript
function makeCountry(name, continent, visited = false) {
  return {
    name,
    continent,
    visited,
    getDescription() {
      let message = `${this.name} is located in ${this.continent}.`;
      message += this.visited ? ' I have visited this country' : 'I have not visited this country';
      console.log(message);
    },
    visitCountry() {
      this.visited = true;
    }
  }
}
let chile = makeCountry('The Republic of Chile', 'South America');
let canada = makeCountry('Canada', 'North America');
let southAfrica = makeCountry('The Republic of South Africa', 'Africa');

// chile.getDescription();       // "The Republic of Chile is located in South America."
canada.getDescription();      // "Canada is located in North America."
canada.visitCountry();
canada.getDescription();      // "Canada is located in North America."
// southAfrica.getDescription(); // "The Republic of South Africa is located in Africa."
```

### [12	Object Orientation](https://launchschool.com/lessons/4671d66f/assignments/d60424ee)

- all familiar

### [13	Practice Problems: Object Orientation](https://launchschool.com/lessons/4671d66f/assignments/1b026797)

```javascript
function createProduce(id, name, stock, price) {
  let newProduct = {};
  newProduct.id = id;
  newProduct.name = name;
  newProduct.stock = stock;
  newProduct.price = price;
  newProduct.describe = function() {
    console.log(`=> Name: ${this.name}`);
    console.log(`=> ID: ${this.id}`);
    console.log(`=> Price: ${this.price}`);
    console.log(`=> Stock: ${this.stock}`);
  };
  newProduct.setPrice = function(newPrice) {
    if (newPrice < 0) {
      console.log('price too low');
    } else {
      this.price = newPrice;
      console.log(`${this.name} is now $${this.price}`);
    }
  }
  return newProduct;
}

let scissors = createProduce(1, 'Scissors', 8, 20);
let drill = createProduce(2, 'Big Drill', 20, 30);
drill.describe();
drill.setPrice(20)
```

### 14	Summary

## [3 Function Contexts and Objects](https://launchschool.com/lessons/c9200ad2/assignments)

- Unline most mainstream OO languages, Javascript has **first class functions**, which means:
  - They can be added to (and removed from) objects.
  - They can be executed in the context of those objects
  - They can be passed to other functions.
  - They initially have no context and only receive one when the program executes.

### Introduction
### [Prerequisites](https://launchschool.com/lessons/c9200ad2/assignments/a29e48d9)

- [Strict mode](https://launchschool.com/gists/406ba491)

### [The Global Object](https://launchschool.com/lessons/c9200ad2/assignments/c8e3c9a4)

- When we declare variables with `var` or `function` they become properties of the global object, like if they were declared without a key-word. (Not so with `let`)
- In non-browser javascript environments the global object is `global`
- Node.js files have a "module scope". variables defined with `var` or `let` use this scope as their context, where variables defined without use the global scope and are visible outside the file.
- All variables and functions in node have their own scope because node files are wrapped in a function that look like this:
```javascript
(function (exports, require, module, __filename, __dirname) {
   // your code is here
});
```

- [Chrome Snippets](https://techtldr.com/using-code-snippets-in-chrome-developer-tools/)
- In strict mode undeclared variables cannot be used. This protects agaoinst mis-spellings accidentally creating new variables.

### Practice Problems: The Global Object

1. `Window {window: Window, self: Window, document: document, name: '', location: Location, …}`
2. 
```javascript
a = 10;
console.log(window.a === a); // true
```
3. 
```javascript
"use strict"

a = 10; // error

console.log(window.a === a);
```
4. 
```javascript
function func() {
  let b = 1;
}

func();

console.log(b); // Reference error
```
5. 
This is allowed because `b` is not declared ? I need to come back to this.
```javascript
function func() {
  b = 1;
}

func();

console.log(b);
```
6.
```
"use strict"

function func() {
  b = 1;
}

func();

console.log(b); // reference error
```
- initially this wasn't returning the error. Then I realised snippets still ahd access to `b` from the previous exercises.

### [Implicit and Explicit Function Execution Contexts](https://launchschool.com/lessons/c9200ad2/assignments/4cc36fd6)

#### Implicit Execution Context for Functions

- Every time a Javascript function is invoked, it has access to an object called the **execution context**
- Implicit v Explicit execution context.
- The rules for variable scope are totally seperate and different to the rules for `this`. This is demonstrated below:
```javascript
"use strict";

function foo() {
  console.log('this here is: ' + this);
}

foo();                // "this here is: undefined"
console.log('this here is: ' + this); // "this here is: [object Window]"
```
#### Implicit Execution Context for Methods

- Remember it's defined bby where the function is called. See below:

```javascript
let foo = {
  bar() {
    return this;
  },
};

let baz = foo.bar;

baz() === foo;    // false
baz() === window; // true
```

#### Explicit execution context 

- We can use `call` and `apply` to change the execution context when calling a function.

```javascript
a = 1;

let obj = {
  a: 'hello',
  b: 'world',
}

function foo() {
  return this.a;
}

console.log(foo()); // 1
console.log(foo.call(obj)); // hello
```

- `apply()` is identical to `.call()` except that it takes an array as the 2nd argument to passs in args.
- Call: count the commas (because the number of arguments needs to match.
- Apply: Arguments as array.

### [Practice Problems: Implicit and Explicit Function Execution Contexts](https://launchschool.com/lessons/c9200ad2/assignments/84fbe7cb)

1. I got it wrong - it is not the foo function:
```javascript
function foo() {
  return this;
}

let context = foo();
console.log(context); // Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
```

2. undefined (correct) when the previous code is run in strict mode.
3. obj object (correct)
```javascript
let obj = {
  foo() {
    return this;
  },
};

let context = obj.foo();

console.log(context);
```
4. 
```javascript
var message = 'Hello from the global scope!';

function deliverMessage() {
  console.log(this.message);
}

deliverMessage();

let bar = {
  message: 'Hello from the function scope!',
};

bar.deliverMessage = deliverMessage;

bar.deliverMessage();
```

My Answer:
- 'Hello from the global scope!'
- ReferenceError -> bar.deliverMessage does not exist
  -  Wrong -> correct answer: Hello from the function scope!

- I need to come back to this, I don't get it.

6. call and apply  (correct)

7.
```javascript
let foo = {
  a: 1,
  b: 2,
};

let bar = {
   a: 'abc',
   b: 'def',
   add() {
     return this.a + this.b;
   },
};

bar.add.call(foo); // 3
```

8. outputList.apply(fruitsObj, fruitsObj.list); (peeked)
9. `slice()` makes a copy of the list of fruits so that each can be handled individually later.
  - Yes but more than that `arguments` is only an array-like object. It has indices from 0 on so it can be iterated over, but one could not call `forEach` on it.

### [Hard Binding Functions with Contexts](https://launchschool.com/lessons/c9200ad2/assignments/bb359c53)

- `bind`:

```javascript
let object = {
  a: 'hello',
  b: 'world',
  foo() {
    return this.a + ' ' + this.b;
  },
};

let bar = object.foo;
bar();                                // "undefined undefined"

let baz = object.foo.bind(object);
baz();                                // "hello world"

let object2 = {
  a: 'hi',
  b: 'there',
};

baz.call(object2);  // "hello world" - `this` is still `object`
```

- bind is non-mutating. it returns a new function.

### [Example: Changing Function Context](https://launchschool.com/lessons/c9200ad2/assignments/b2b3d375)

- I need to go over this again. Broadly I get it, but the finer points washed over me.

### [Practice Problems: Hard Binding Functions with Contexts](https://launchschool.com/lessons/c9200ad2/assignments/5f5647a7)

1. bind
2. Nothing. Bind prints nothing, it returns a new function:
```javascript
let obj = {
  message: 'JavaScript',
};

function foo() {
  console.log(this.message);
}

foo.bind(obj);
```
3. 5
4. Not sure what's happening here.
5. Amazebulous! (correct)

###	[Dealing with Context Loss (1)](https://launchschool.com/lessons/c9200ad2/assignments/013f9f02)

#### Method Losing Context when Taken Out of Object

- **hard binding** (not sure how this is different from normal binding

```javascript
function repeatThreeTimes(func) {
  func();
  func();
  func();
}

function foo() {
  let john = {
    firstName: 'John',
    lastName: 'Doe',
    greetings() {
      console.log('hello, ' + this.firstName + ' ' + this.lastName);
    },
  };

  repeatThreeTimes(john.greetings.bind(john));
}

foo();

// => hello, John Doe
// => hello, John Doe
// => hello, John Doe
```
 
### [Dealing with Context Loss (2)](https://launchschool.com/lessons/c9200ad2/assignments/022f50f4)

```javascript
let obj = {
  a: 'hello',
  b: 'world',
  foo() {
    console.log(this.a + ' ' + this.b); // hello world
    function bar() {
      console.log(this.a + ' ' + this.b); // undefined undefined
    }

    bar();
  },
};

obj.foo();
```

#### Solution 1: Preserve Context with a Local Variable in the Lexical Scope

SELF
`let self = this`

#### Solution 2: Pass the Context to Internal Functions

CALL/APPLY
- ie use `call` or `apply` to pass in `this`

```javascript
let obj = {
  a: 'hello',
  b: 'world',
  foo() {
    function bar() {
      console.log(this.a + ' ' + this.b);
    }

    bar.call(this);
  }
};

obj.foo();
> hello world
```
#### Solution 3: Bind the Context with a Function Expression

BIND
```JAVASCRIPT
let obj = {
  a: 'hello',
  b: 'world',
  foo() {
    let bar = function() {
      console.log(this.a + ' ' + this.b);
    }.bind(this);

    // some lines of code

    bar();

    // more lines of code

    bar();

    // ...
  }
};

obj.foo();
// > hello world
// > hello world
```
- I'm not sure why it the `bar` method needs to be called twice to demonstrate this.

#### Solution 4: Using an Arrow Function

=>

```javascript
let obj = {
  a: 'hello',
  b: 'world',
  foo() {
    let bar = () => console.log(this.a + ' ' + this.b);
    bar();
  }
};

obj.foo();
> hello world
```

- this makes instinctive sense to me because when using braces with a method like `reduce` one needs to return the value, but not so with arrow functions.


### [Dealing with Context Loss (3)](https://launchschool.com/lessons/c9200ad2/assignments/f68a9f7f)

- This page seems like it's covering exactly the asme material as the previous page?
- With the exception of: 'the optional thisArg argument'
  - `map`, `every`, `some` and `forEach` have an optional context argument, making the following possible:
```javascript
let obj = {
  a: 'hello',
  b: 'world',
  foo() {
    [1, 2, 3].forEach(function(number) {
      console.log(String(number) + ' ' + this.a + ' ' + this.b);
    }, this);
  },
};

obj.foo();

// => 1 hello world
// => 2 hello world
// => 3 hello world
```

### [Practice Problems: Dealing with Context Loss](https://launchschool.com/lessons/c9200ad2/assignments/92892280)

1. Reference error, incorrect, actually `undefined undefined is a undefined.`

```javascript
let turk = {
  firstName: 'Christopher',
  lastName: 'Turk',
  occupation: 'Surgeon',
  getDescription() {
    return this.firstName + ' ' + this.lastName + ' is a ' + this.occupation + '.';
  }
};

function logReturnVal(func) {
  let returnVal = func();
  console.log(returnVal);
}

logReturnVal(turk.getDescription);
```
- I didn't know that calling a non-existent property on an object returns `undefined` rather than a reference error.

2. correct

```javascript
let turk = {
  firstName: 'Christopher',
  lastName: 'Turk',
  occupation: 'Surgeon',
  getDescription() {
    return this.firstName + ' ' + this.lastName + ' is a ' + this.occupation + '.';
  }
};

function logReturnVal(func, context) {
  let returnVal = func.apply(context);
  console.log(returnVal);
}

logReturnVal(turk.getDescription, turk);
```
3.
```javascript
let turk = {
  firstName: 'Christopher',
  lastName: 'Turk',
  occupation: 'Surgeon',
  getDescription() {
    let foo = function() {
      return this.firstName + ' ' + this.lastName + ' is a ' + this.occupation + '.';
    }.bind(turk)
    return foo();
  }
};

function logReturnVal(func) {
  let returnVal = func();
  console.log(returnVal);
}

let getTurkDescription = turk.getDescription;
console.log(getTurkDescription());
```

LS solution

```javascript
let turk = {
  firstName: 'Christopher',
  lastName: 'Turk',
  occupation: 'Surgeon',
  getDescription() {
    return this.firstName + ' ' + this.lastName + ' is a ' + this.occupation + '.';
  }
};

function logReturnVal(func) {
  let returnVal = func();
  console.log(returnVal);
}

let getTurkDescription = turk.getDescription.bind(turk);
console.log(getTurkDescription())
```

4. Yes it will print the desired output, because `let` (not `var` or `function`) creates a local scope that attaches its functions to their context when `this` is invoked.
- incorrect
- The function arguments lose their surrounding context.

```javascript
let TESgames = {
  titles: ['Arena', 'Daggerfall', 'Morrowind', 'Oblivion', 'Skyrim'],
  seriesTitle: 'The Elder Scrolls',
  listGames() {
    this.titles.forEach(function(title) {
      console.log(this.seriesTitle + ' ' + title);
    });
  }
};

TESgames.listGames();

// undefined Arena
// undefined Daggerfall
// undefined Morrowind
// undefined Oblivion
// undefined Skyrim
```

5. Correct

```javascript
let TESgames = {
  titles: ['Arena', 'Daggerfall', 'Morrowind', 'Oblivion', 'Skyrim'],
  seriesTitle: 'The Elder Scrolls',
  listGames() {
    this.titles.forEach((title) => console.log(this.seriesTitle + ' ' + title));
  }
};

TESgames.listGames();

// undefined Arena
// undefined Daggerfall
// undefined Morrowind
// undefined Oblivion
// undefined Skyrim
```

6. + 7. correct - well actually this was the solution to exercise 7. The LS soluton I have put below.
```javascript
let TESgames = {
  titles: ['Arena', 'Daggerfall', 'Morrowind', 'Oblivion', 'Skyrim'],
  seriesTitle: 'The Elder Scrolls',
  listGames() {
    let self = this;
    this.titles.forEach(function(title) {
      console.log(this.seriesTitle + ' ' + title);
    }, this);
  }
};

TESgames.listGames();
```

```javascript
let TESgames = {
  titles: ['Arena', 'Daggerfall', 'Morrowind', 'Oblivion', 'Skyrim'],
  seriesTitle: 'The Elder Scrolls',
  listGames() {
    let self = this;
    this.titles.forEach(function(title) {
      console.log(self.seriesTitle + ' ' + title);
    });
  }
};
```
8. It won't work, because of context loss, so 0
9. 

```javascript
let foo = {
  a: 0,
  incrementA() {
    let self = this;
    function increment() {
      self.a += 1;
    }

    increment();
  }
};

foo.incrementA();
foo.incrementA();
foo.incrementA();
console.log(foo.a)
```

10.

```javascript
let foo = {
  a: 0,
  incrementA() {
    let increment = function() {
      this.a += 1;
    }.bind(foo)

    increment.apply(this);
    increment.apply(this);
    increment.apply(this);
  }
};

foo.incrementA();
console.log(foo.a)
```
### [Summary: The this Keyword in JavaScript](https://launchschool.com/lessons/c9200ad2/assignments/76bc0829)


### [Practice Problems: What is this? (1)](https://launchschool.com/lessons/c9200ad2/assignments/82f593ef)](https://launchschool.com/lessons/c9200ad2/assignments/82f593ef)

- rushed

### [Practice Problems: What is this? (2)](https://launchschool.com/lessons/c9200ad2/assignments/7bef6908)

1.
- my answer:
  -  In the object declaration `this` points to its containing object, which is `myChildObject`. When the `myMethod()` method is called it points to `myObject`. The method returns 1. (incorrect)
  -  LS answer: this is myChildObject, which means this.count is undefined, so the return value is undefined.

```javascript
let myObject = {
  count: 1,
  myChildObject: {
    myMethod() {
      return this.count;
    },
  },
};

let r = myObject.myChildObject.myMethod();
console.log(r) // undefined
```

2.

`myObject.myChildObject.myMethod.call(myObject);`

3. An error because `bind` must be invoked at declaration, not execution. (incorrect)

```javascript
let person = {
  firstName: 'Peter',
  lastName: 'Parker',
  fullName() {
    console.log(this.firstName + ' ' + this.lastName +
                ' is the Amazing Spiderman!');
  },
};

let whoIsSpiderman = person.fullName.bind(person); //Peter Parker is the Amazing Spiderman!
whoIsSpiderman();
```

4.
```javascript
let computer = {
  price: 30000,
  shipping: 2000,
  total() {
    let tax = 3000;
    let specialDiscount = function() {
      if (this.price > 20000) {
        return 1000;
      } else {
        return 0;
      }
    }.bind(computer)

    return this.price + this.shipping + tax - specialDiscount();
  }
};

console.log(computer.total());
```


### Summary
### Quiz

- 6/9 14.3.25

## [4 Closures and Function Scope](https://launchschool.com/lessons/0b371359/home)

### [Function and Scope Review	](https://launchschool.com/lessons/0b371359/assignments/613bd3bb)

- 

### [Higher-Order Functions](https://launchschool.com/lessons/0b371359/assignments/f5b3f244)

- A higher order function is one that takes a function, returns a function, or both.

```javascript
function timed(func) {
  return function() {
    let start = new Date();
    func();
    let stop = new Date();
    console.log((stop - start).toString() + ' ms have elapsed');
  };
}
```

- Note that first class functions are not the same as higehr order functions [link](https://stackoverflow.com/questions/10141124/any-difference-between-first-class-function-and-high-order-function)
  - "There is a difference. When you say that a language has first-class functions, it means that the language treats functions as values – that you can assign a function into a variable, pass it around etc. Higher-order functions are functions that work on other functions, meaning that they take one or more functions as an argument and can also return a function.

The “higher-order” concept can be applied to functions in general, like functions in the mathematical sense. The “first-class” concept only has to do with functions in programming languages. It’s seldom used when referring to a function, such as “a first-class function”. It’s much more common to say that “a language has/hasn’t first-class function support”.

The two things are closely related, as it’s hard to imagine a language with first-class functions that would not also support higher-order functions, and conversely a language with higher-order functions but without first-class function support."

### [Practice Problems: Higher-Order Functions](https://launchschool.com/lessons/0b371359/assignments/a4544340)

1. have functions as either argument or return value.(correct)
2. filter
3.
```javascript
let numbers = [1, 2, 3, 4];
function makeCheckEven() {
  return (n) => n % 2 === 0;
}

let checkEven = makeCheckEven();
let r = numbers.filter(checkEven); // [2, 4]
console.log(r)
```
4.
```javascript
function execute(func, operand) {
  console.log(func(operand));
}

execute(function(number) {
  return number * 2;
}, 10); // 20

execute(function(string) {
  return string.toUpperCase();
}, 'hey there buddy'); // "HEY THERE BUDDY"
```
5. 
```javascript
function makeListTransformer(func) {
  return (array) => array.map((n) => func(n))
//return (array) => array.map(func) -> LS solution
}

let timesTwo = makeListTransformer(function(number) {
  return number * 2;
});

let r = timesTwo([1, 2, 3, 4]); // [2, 4, 6, 8]

console.log(r)
```
### [Closures and Private Data](https://launchschool.com/lessons/0b371359/assignments/7bd21ae8)

```javascript
function makeCounter() {
  let count = 0;       // declare a new variable
  return function() {
    count += 1;        // references count from the outer scope
    console.log(count);
  };
}

let counter = makeCounter();
counter(); // 1
counter(); //2
counter(); //3
```

- The code above makes `count` a private variable, only accessible via the `counter()` function.

1.

```javascript
function makeCounter() {
  let count = 0;       // declare a new variable
  return function() {
    count += 1;        // references count from the outer scope
    console.log(count);
  };
}

function makeCounterLogger(num1) {
  return function(num2) {
    let n1Copy = num1;
    if (n1Copy === num2) console.log(n1Copy);
    if (n1Copy > num2) {
      while (n1Copy >= num2) {
        console.log(n1Copy);
        n1Copy--
      } 
    } else {
      while (n1Copy <= num2) {
        console.log(n1Copy);
        n1Copy++
      } 
    }
  }
}

let countlog = makeCounterLogger(5);
countlog(8);
// 5
// 6
// 7
// 8
countlog(2);
// 5
// 4
// 3
// 2
```

2. (I found this unneccessarily difficult - am I exhausted?)
```javascript

function makeList() {
  let items = []
  return function (newItem) {
    let index;
    if (newItem) {
      index = items.indexOf(newItem);
      if (index === -1) {
        items.push(newItem);
        console.log(newItem + ' added!');
      } else {
        items.splice(index, 1);
        console.log(newItem + ' removed!')
      }
    } else {
      if (items.length === 0) {
        console.log('list empty!');
      } else {
        items.forEach((i) => console.log(i))
      }
    }
  }
}

let list = makeList();
list() // 'The list is empty.
list('make breakfast')
list('read book')
list();
// make breakfast
// read book
list('make breakfast');
// make breakfast removed!
list();
// read book
```

### [Practice Problems: Closures	](https://launchschool.com/lessons/0b371359/assignments/5271e93c)

1. 
```javascript
function makeMultipleLister(num) {
  return function() {
    let starter = num;
    while (starter < 100) {
      console.log(starter);
      starter += num;
    }
  }
}
```
2. I thought this was cheating, but it turns out this was what LS had in mind

```javascript
   number = 0;

function add(n) {
  return number += n;
}

function subtract(n) {
  return number -= n;
}

console.log(add(1));
// 1
console.log(add(42));
// 43
console.log(subtract(39));
// 4
console.log(add(6));
// 10
```

3. There is no way to access `status` from outside the function.

```javascript
function startup() {
  let status = 'ready';
  return function() {
    console.log('The system is ready.');
  };
}

let ready = startup();
let systemStatus = // ?
```

### [Objects and Closures](https://launchschool.com/lessons/0b371359/assignments/621678ef)

1.

```javascript
function makeList() {
  return {
    items: [],
    index: 0,
    add: function (newItem) {
      if (newItem) {
        index = this.items.indexOf(newItem);
        if (index === -1) {
          this.items.push(newItem);
          console.log(newItem + ' added!');
        } else {
          console.log('error: item already on the list')
        }
      } else {
        console.log('error: you failed to pass in an item')
      }
    },
    list: function() {
      if (this.items.length === 0) {
        console.log('The list is empty.');
      } else {
        this.items.forEach(function(item) {
          console.log(item);
        });
      }
    },
    remove: function (newItem) {
      if (newItem) {
        index = this.items.indexOf(newItem);
        if (index === -1) {
          console.log('error, item not on the list');
        } else {
          this.items.splice(index, 1);
          console.log(newItem + ' removed!');
        }
      } else {
        console.log('error: you didn\'t pass in an argument')
      }
    }
  }
}
let list = makeList();
list.add('peas');
// peas added!
list.list();
// peas
list.add('corn');
// corn added!
list.list();
// peas
// corn
list.remove('peas');
// peas removed!
list.list();
// corn
```

2.

```javascript
function makeList() {
  let items = [];
  let index = 0;
  return {
    add: function (newItem) {
      if (newItem) {
        index = items.indexOf(newItem);
        if (index === -1) {
          items.push(newItem);
          console.log(newItem + ' added!');
        } else {
          console.log('error: item already on the list')
        }
      } else {
        console.log('error: you failed to pass in an item')
      }
    },
    list: function() {
      if (items.length === 0) {
        console.log('The list is empty.');
      } else {
        items.forEach(function(item) {
          console.log(item);
        });
      }
    },
    remove: function (newItem) {
      if (newItem) {
        index = items.indexOf(newItem);
        if (index === -1) {
          console.log('error, item not on the list');
        } else {
          items.splice(index, 1);
          console.log(newItem + ' removed!');
        }
      } else {
        console.log('error: you didn\'t pass in an argument')
      }
    }
  }
}
let list = makeList();
list.add('peas');
// peas added!
list.list();
// peas
list.add('corn');
// corn added!
list.list();
// peas
// corn
list.remove('peas');
// peas removed!
list.list();
// corn
console.log(list.items);
```

#### Why use closures to make data private?

- restricts data in a good way that forces other devs to use the intended interface.
- data-integrity.
- a disadvantage of this is that it can make it harder to extend the code, for instance here with a `clear` method.
### [Project: Banking with Objects and Closures](https://launchschool.com/lessons/0b371359/assignments/e071c151)

- My code diverted from the LS solution quite a bit by the end.
```
function makeAccount(currID) {
  return {
    transactionsVar: [],
    transactions: function() {
      return this.transactionsVar;
    },
    numberVar: currID,
    number: function() {
      return this.numberVar;
    },
    recordTransaction: function(type, amount) {
      this.transactionsVar.push({
        type,
        amount,
      });
    },
    balanceVar: 0,
    balance: function() {
      return this.balanceVar;
    },
    deposit: function(amount) {
      this.balanceVar += amount;
      this.recordTransaction('deposit', amount);
      return amount;
    },
    withdraw: function(amount) {
      if (amount > this.balanceVar) {
        console.log('insufficient funds');
        this.balanceVar -= this.balanceVar;
        this.recordTransaction('withdraw', this.balanceVar -= this.balanceVar);
        return 0;
      } else {
        this.balanceVar -= amount;
        this.recordTransaction('withdraw', this.balanceVar - amount);
        return amount;
      }
    }
  }
}

function makeBank() {
  return {
    accounts: [],
    currID: 100,
    openAccount() {
      let newAccount = makeAccount(this.currID += 1);
      this.accounts.push(newAccount);
      return newAccount;
    },
    transfer(from, to, amount){
      return to.deposit(from.withdraw(amount));    
    },
  }
};

let bank = makeBank();
let account = bank.openAccount();
console.log(account.balance());
// 0
console.log(account.deposit(17));
// 17
let secondAccount = bank.openAccount();
console.log(secondAccount.number());
// 102
console.log(account.transactions());
// [{...}]
console.log(bank.accounts);
```

- LS code:

```javascript
function makeBank() {
  let accounts = [];

  function makeAccount(number) {
    let balance = 0;
    let transactions = [];

    return {
      deposit(amount) {
        transactions.push({type: "deposit", amount: amount});
        balance += amount;
        return amount;
      },

      withdraw(amount) {
        if (amount > balance) {
          amount = balance;
        }

        transactions.push({type: "withdraw", amount: amount});
        balance -= amount;
        return amount;
      },

      balance() {
        return balance;
      },

      number() {
        return number;
      },

      transactions() {
        return transactions;
      },
    };
  }

  return {
    openAccount() {
      let number = accounts.length + 101;
      let account = makeAccount(number);
      accounts.push(account);
      return account;
    },

    transfer(source, destination, amount) {
      return destination.deposit(source.withdraw(amount));
    },
  };
}
```
### [Garbage Collection](https://launchschool.com/lessons/0b371359/assignments/48d2a179)

- As long as a variable remains accessible Javascript can't free up that piece of memory for garbage collection.

#### The stack and heap

- not all values in JS are garbage-collected.
- When primitve values are stored in the stack, they are not garbage collected.
- GC doesn't mean the variable going out of scope - this is a common confusion.

#### Why Do You Need To Know About Garbage Collection

- Modern javascript uses a Mark and Sweep algorithm to garbage collect. (collects all non-reachable objects)

### [How Closures Affect Garbage Collection](https://launchschool.com/lessons/0b371359/assignments/c19c9fbf)

- "dereferences"

#### Problems

1. 
- `let a = [1]` is initialized on the global object and so reachable for the life of the program.
  - No - you failed to see that `a` is reassigned on line 4 because the `a` variable there can see the top level and so is not an independent function variable.
  - 
- [ 1, 2] is assigned to `a` within the `add()` function and is garbage collected after that function has run. Concat is non-mutating.
- `[2]` is unreachable outside `run()` and `add()` so GC happens after the two functions have completed.
  - yes
2. Never? no, after the program finishes.
  
### [Practice Problems: Garbage Collection](https://launchschool.com/lessons/0b371359/assignments/d5156138)

1. Yes it is. That means it takes care of deleting references to unreachable variables without the dev having to write any code to do so.
2. `myArr` is GC on line 5 / `1` is a primitive value so not garbage collected, but `myNum` is GC when the program finishes.
   -  sort of, you're logic is sound, but `myArr` is GC on line 10 after the `foo` function is finished.
3. No - because I can still access it via the `greeting` object, like this: console.log(greeting())
### [Partial Function Application](https://launchschool.com/lessons/0b371359/assignments/f2c6f687)

- We learnt this in JS210 ([link](https://launchschool.com/lessons/0b371359/assignments/f2c6f687))
- vocab (don't need to learn - they're chapter specific):
  - the generator (function)
  - the applicator (function)
  - the primary (function)

```javascript
function partial(primary, arg1) {
  return function(arg2) {
    return primary(arg1, arg2);
  };
}

function greet(n1, n2) {
  let first = n1[0].toUpperCase() + n1.slice(1);
  let second = n2[0].toUpperCase() + n2.slice(1); 
  console.log(first + ', ' + second + '!')
}

let sayHello = partial(greet, 'Hello');
let sayHi = partial(greet, 'Hi');

sayHello('Brandon');
// Hello, Brandon!
sayHi('Sarah');
// Hi, Sarah!
```

### [Practice Problems: Partial Function Application](https://launchschool.com/lessons/0b371359/assignments/4cb22406)

1.

```javascript
function subtract(a, b) {
  return a - b;
}

function makeSub() {
  return function(a) {
    return subtract(a, 5);
  }
}

const sub5 = makeSub();

sub5(10); // 5
sub5(20); // 15
```

2. 

```javascript
function makeSubN(n1) {
  return function(n2) {
    console.log(n2 - n1);
  }
}
```

3.
```javascript
function makePartialFunc(func, b) {
  return function(a) {
    console.log(func(a, b));
  }
}
```

4. The closure includes and retains access to `multiply` when it is called on line 15. - incomplete answer:
  - yes, closures, but no to exectuion. In fact, when a new function is created, it retains access to any variables that are defined in the function's outer scope.

5. 
```javascript
function makeMathRollCall() {
  return function(entry) {
    rollCall('Math', entry)
  }
}
```


### [Immediately Invoked Function Expressions](https://launchschool.com/lessons/0b371359/assignments/9c1daec2)	

- **IIFE**

### [Creating a Private Scope with an IIFE](https://launchschool.com/lessons/0b371359/assignments/f27fd52c)

- An example is given where one must contribute to a large and messay file. You want to create a `myPet` variable, but aren't sure if one already exists. So you hide your new code within a function, like this:

```javascript
function createAndLogPet() {
  var myPet = {
    type: 'Dog',
    name: 'Spot',
  };

  console.log(`I have pet ${myPet.type} named ${myPet.name}`);
}
```
- LS asks  what the problem with this code is. myANswer:
  - the function can create multiple identical pets without the ability to change its name or type
  - or... something to do with `var` ?
    - no, as in the previous problem, we do not know whether a function called createAndLogPet already exists.
- we can solve this problem by making it a IIFE :

```javascript
// thousands of lines of messy JavaScript code!

(function() {
  var myPet = {
    type: 'Dog',
    name: 'Spot',
  };

  console.log(`I have pet ${myPet.type} named ${myPet.name}`);
})();

// more messy JavaScript code
```

- (also allowing us to pass in arguments)

```javascript
// thousands of lines of messy JavaScript code!

(function(type, name) {
  var myPet = {
    type,
    name,
  };

  console.log(`I have pet ${myPet.type} named ${myPet.name}`);
})('Dog', 'Spot');

// more messy JavaScript code
```

### [Creating Private Data with an IIFE](https://launchschool.com/lessons/0b371359/assignments/470d67c3)

#### Using an IIFE to Return a Function with Access to Private Data

```javascript
let generateStudentId = (function() {
  let studentId = 0;

  return function() {
    studentId += 1;
    return studentId;
  };
})();

generateStudentId();          // 1
generateStudentId();          // 2
generateStudentId();          // 3
```

#### Using an IIFE to Return an Object with Private Data

- This is not going in - I must come back.

### [Practice Problems: IIFEs](https://launchschool.com/lessons/0b371359/assignments/224707db)

1.error
2. 
```javascript
(function() {
  console.log("Sometimes, syntax isn't intuitive!")
})();
```
3. The problem is that it is reassigning `sum`, so when we try and call the function it is no longer a function. This is variable shadowing because the writer has inadvertantly used a name that already existed in the code-base. I will fix it with IIFE below:

```javascript
var sum = 0;
var numbers;

sum += 10;
sum += 31;

numbers = [1, 7, -3, 3];

sum += (function(arr) {
  return arr.reduce(function(sum, number) {
    sum += number;
    return sum;
  }, 0);
})(numbers);  // ?

console.log(sum)
sum += sum(numbers);  // ?
```

4. 
```javascript
function countdown(count) {
  return function(n) {
    while (n >= 0) {
      console.log(n--);
    }
    console.log('Done!');
  }(count);
};

countdown(7);
// 7
// 6
// 5
// 4
// 3
// 2
// 1
// 0
// Done!
```
5. no?
6. nailed it
```javascript
function countdown(count) {
  if (count < 0) {
    console.log('Done!')
    return;
  } else {
    (function(count) {
      console.log(count);
      countdown(count-1);
    })(count);
  }
}

countdown(7)
```

### [Summary](https://launchschool.com/lessons/0b371359/assignments/7cc229dd)

-

### Quiz	

- 6/7 (17.3.25)

## [5 Object Creation Patterns](https://launchschool.com/lessons/24a4613a/assignments)

### [Introduction](https://launchschool.com/lessons/24a4613a/assignments/71d1df25)



### [Finish Reading the OO JavaScript Book](https://launchschool.com/lessons/24a4613a/assignments/fefebb19)


### [Factory Functions](https://launchschool.com/lessons/24a4613a/assignments/d76ba762)

#### Factory Functions



### [Practice Problems: Create Objects with Factory Functions](https://launchschool.com/lessons/24a4613a/assignments/4b9d7572)

1.

- There's no way to test what factory produced them and so what type of object they are
- All methods are coppied which can lead to redundancy

2.

```javascript
function makeObj() {
  return {
    propA: 10,
    propB: 20,
  }
}
```

3.

```javascript
function createInvoice(invoice = {}) {
  return {
    phone: invoice.phone ? invoice.phone : 3000,
    internet: invoice.internet ? invoice.internet : 5500,
    total() {
      return this.phone + this.internet;
    }
  }
}
```

LS solution similar:

```javascript
function createInvoice(services={}) {
  return {
    phone: services.phone || 3000,
    internet: services.internet || 5500,
    total: function() {
      return this.phone + this.internet;
    },
  };
}
```

4. 

```javascript
function createInvoice(services={}) {
  let invoice = {
    amount: services.amount || 0,
    phone: services.phone || 0,
    internet: services.internet || 0,
  };

  invoice.total = function() {
    return this.phone + this.internet + this.amount;
  };

  return invoice;
}

function createPayment(services) {
  return createInvoice(services);
}
```

5.

```javascript
function createInvoice(services={}) {
  return {
    phone: [services.phone || 0],
    internet: [services.internet || 0],
    amount: [services.amount || 0],
    addPayment: function(payment) {
      this.phone -= payment.phone;
      this.internet -= payment.internet;
      this.amount -= payment.amount || 0;
    },
    addPayments: function(payments) {
      for (i = 0; i < payments.length; i++) {
        // console.log(payments[i])
        this.addPayment(payments[i])
      }
    },
    amountDue: function() {
      return Number(this.phone) + Number(this.internet) + Number(this.amount);
    }
  };
}

function createPayment(services) {
  services = services || {};
  return {
    phone: services.phone || 0,
    internet: services.internet || 0,
    amount: services.amount,
    total: function() {
      return this.amount || (this.phone + this.internet);
    },
  };
}

let invoice = createInvoice({
  phone: 1200,
  internet: 4000,
});

let payment1 = createPayment({
  amount: 2000,
});

let payment2 = createPayment({
  phone: 1000,
  internet: 1200,
});

let payment3 = createPayment({
  phone: 1000,
});

invoice.addPayment(payment1);

invoice.addPayments([payment2, payment3]);

let a = invoice.amountDue();       // this should return 0

```


### [Constructor Pattern](https://launchschool.com/lessons/24a4613a/assignments/c659f8e4)

- what is going on here...

```javascript
// constructor function
function Person(firstName, lastName='') {
  this.firstName = firstName;
  this.lastName = lastName;
  this.fullName = function() {
    return (this.firstName + ' ' + this.lastName).trim();
  };
}

let john = new Person('John', 'Doe');
let jane = new Person('Jane');

console.log(john.fullName());              // "John Doe"
console.log(jane.fullName());              // "Jane"

console.log(john.constructor);             // function Person(..)
console.log(jane.constructor);             // function Person(..)

console.log(john instanceof Person);       // true
console.log(jane instanceof Person);       // true
```

#### Problems

1. Capitalised
2. error because Lizzy is undefined
3. `let lizzy = new Lizard();`

### [Objects and Prototypes](https://launchschool.com/lessons/24a4613a/assignments/da0992e3)

- ok

#### The __proto__ Property

- "dunder"

#### Prototype Chain and the Object.prototype Object

#### Problems:

1. `let foo = Object.create(prot);`
2. `console.log(Object.getPrototypeOf(foo) === prot)`
3. `console.log(prot.isPrototypeOf(foo))`
4. got this wrong. the 2nd returns true because Object.prototype is on the prototype chain of foo.

### [Prototypal Inheritance and Behavior Delegation](https://launchschool.com/lessons/24a4613a/assignments/7143264c)

#### Prototype Chain Lookup for Property Access

- ok

#### Prototypal Inheritance and Behavior Delegation

- 

#### Overriding Default Behavior

- Objects defined from the same prototype can override methods by defining methods with the same name locally.

```javascript
let dog = {
  say() {
    console.log(this.name + ' says Woof!');
  },
};

let fido = Object.create(dog);
fido.name = 'Fido';
fido.say = function() {
  console.log(this.name + ' says wassup!');
};

fido.say();
let spot = Object.create(dog);
spot.name = 'Spot';
spot.say()
```

#### Object.getOwnPropertyNames and object.hasOwnProperty



#### Methods on Object.prototype

#### Problems:

1. `1`
2. `2`
3. (I got wrong)

### [Practice Problems: Prototypes and Prototypal Inheritance](https://launchschool.com/lessons/24a4613a/assignments/b158be5a)

1.

```javascript
function getDefiningObject(object, propKey) {
  if (Object.is(object, null) || Object.hasOwn(object, propKey)) {
    return object;
  } else {
    return getDefiningObject(Object.getPrototypeOf(object), propKey)
  }
}
```

LS solution:

```javascript
function getDefiningObject(object, propKey) {
  while (object && !object.hasOwnProperty(propKey)) {
    object = Object.getPrototypeOf(object);
  }

  return object;
}
```

2. I didn't get there

LS solution:

```javascript
function shallowCopy(object) {
  let result = Object.create(Object.getPrototypeOf(object));

  for (let prop in object) {
    if (object.hasOwnProperty(prop)) result[prop] = object[prop];
  }

  return result;
}
```
3.
```javascript
function extend(output, ...objects) {
  objects.forEach((o) => {
    Object.getOwnPropertyNames(o).forEach(function(prop) {
      output[prop] = o[prop];
    });
  })
  return output;
}
```

### [Function Prototypes and Object Prototypes](https://launchschool.com/lessons/24a4613a/assignments/441a520a)

- ok

### [Constructors, Prototypes, and the Prototype Chain](https://launchschool.com/lessons/24a4613a/assignments/5de6e5a0)

- ok

#### The Constructor prototype Property

- ok
- [article](https://medium.com/@patel.aneeesh/a-shallow-dive-into-the-constructor-property-in-javascript-b0a89747058b)

### [Practice Problems: Constructor Functions and Prototypes (1)](https://launchschool.com/lessons/24a4613a/assignments/2d53f659)

1. got 2 out of 6
2. 
```javascript
console.log(RECTANGLE.area.call(rect1));
console.log(RECTANGLE.perimeter.call(rect1));
```
3. 
```javascript
function Circle(r) {
  return {
    r,
    area: function() {
      return (this.r ** 2)  * Math.PI ;
    }
  }
}
```
4. An error, because where the function is called, `this` refers to the global object. -> incorrect.
5. 

```javascript
Ninja.prototype.swing = function() {
  this.swung = true;
  return this
}
```

6.

My solution: `let ninjaB = Object.create(ninjaA)` , which passes the test case, but isn't correct because, it uses NinjaA as the prototype object, meaning it makes a new object which references NinjaA, rather than creating a new instance of NinjaA.

LS solution: `let ninjaB = Object.create(Object.getPrototypeOf(ninjaA));`

### [Practice Problems: Constructor Functions and Prototypes (2)](https://launchschool.com/lessons/24a4613a/assignments/cbb1afa7)

1. I didn't quite get there on this one:

```javascript

let shape = {
  getType() {
    return this.type;
  },
}

function Triangle(a, b, c) {
  this.type = 'triangle';
  this.a = a,
  this.b = b,
  this.c = c
}

Triangle.prototype = shape;
Triangle.prototype.getPerimeter = function() {
  return this.a + this.b + this.c;
}

let t = new Triangle(3, 4, 5);
console.log(t.constructor);                 // Triangle(a, b, c)
console.log(shape.isPrototypeOf(t));        // true
console.log(t.getPerimeter());              // 12
console.log(t.getType());                   // "triangle"
```

2. My incomplete answer:

```javascript
console.log("Hello".constructor);
console.log([1,2,3].constructor);
console.log({name: 'Srdjan'}.constructor);
```

LS answer:
```
console.log("Hello".constructor.name);
console.log([1,2,3].constructor.name);
console.log({name: 'Srdjan'}.constructor.name);
```

3.

```javasscript
function User(first, last) {
  return {
    name: first + ' ' + last,
  }
}
```
- not quite, I think this early returns which means the `new` constructor doesn't do it's job.
- LS:

```javascript
function User(first, last){
  if (!(this instanceof User)) {
    return new User(first, last);
  }

  this.name = first + ' ' + last;
}
```

4. 

```javascript
function createObject(obj) {
  let output = {};
  Object.setPrototypeOf(output, obj);
  return output;
}
```
- correct, except `setPrototypeOf` is problematic. The LS solution does : `output.prototype = obj;`

5. My answer:

```javascript
Object.prototype.begetObject = function(){
  let output = {};
  Object.setPrototypeOf(output, this);
  return output;
}
```
- yes, but same reservation as last time.
- LS:

```javascript
Object.prototype.begetObject = function () {
  function F() {}
  F.prototype = this;
  return new F();
}
```

6.
```javascript
function neww(constructor, args) {
  let proto = constructor.prototype;
  let output = new constructor(...args);
  output.prototype = proto;
  return output;
}
```

- LS soluton adds a line at the end, which is confusing me. SOmething to do with constructor functions sometimes returning things other than objects, and this being a bad thing...

`return typeof result === 'object' ? result : object;`

### [Static and Instance Properties and Methods](https://launchschool.com/lessons/24a4613a/assignments/158c7550)

- yup

#### Instance Properties

- makes sense. The properties bound to an instance are its instance properties.

#### Instance Methods

- yep. As above. Some of these are stored in the prototype, some on the instance itself, but we can call them all instance methods because they are available on the instance object.  

#### Static Properties

- defined and accessed directly on the constructor
- Can use them to keep track of all instances created, like so:

```javascript
function Dog(name, breed, weight) {
  this.name = name;
  this.breed = breed;
  this.weight = weight;
  Dog.allDogs.push(this);
}

Dog.allDogs = [];
```

#### Static Methods

```javascript
Dog.showSpecies = function() {
  console.log(`Dogs belong to the species ${Dog.species}`);
};

Dog.showSpecies();
```

### [The Pseudo-classical Pattern and the OLOO Pattern](https://launchschool.com/lessons/24a4613a/assignments/b01b636b)

- The pseudo-classical pattern
- The Object Linking to Other Object (OLOO) patttern.

#### Object Creation Considerations

Objects are rarely independent and unique. Therefore We want objects to:
  - Be able to have their own states;
  - Share their behaviors

#### The Pseudo-classical Pattern

- constructor pattern:

```javascript
let Point = function(x = 0, y = 0) {            // capitalized constructor name as a convention
  this.x = x;                                   // initialize states with arguments
  this.y = y;                                   // 0 as default value
};
```

 plus prototype pattern:

 ```javascript

Point.prototype.onXAxis = function() {  // shared behaviors added to constructor's prototype property
  return this.y === 0;
};

Point.prototype.onYAxis = function() {  // these methods are added one by one
  return this.x === 0;
};

Point.prototype.distanceToOrigin = function() {
  return Math.sqrt((this.x * this.x) + (this.y * this.y));
};
```

works just fine:

```javascript
let pointA = new Point(30, 40);         // use new to create objects
let pointB = new Point(20);

pointA instanceof Point;                // use instanceof to check type
pointB instanceof Point;

pointA.distanceToOrigin();              // 50
pointB.onXAxis();                       // true
```

#### The OLOO Pattern

(this is history - you may come across it, but it's not on the exam)

- it's not quite going in...

#### Practice Problems

1. 
```javascript
let PetPrototype = {       
  wake() {
    console.log('I am awake');
  },

  sleep() {
    console.log('I am sleeping')
  },

  init(animal, name) {         
    this.animal = animal;
    this.name = name;
    return this;
  },
};
```

2.
```javascript
let Pet = function(animal, name) {
  this.animal;
  this.name;
}

Pet.prototype.sleep = function() {
  console.log('I am sleeping')
}

Pet.prototype.wake = function() {
  console.log('I am awake')
};

let pudding = new Pet("Cat", "Pudding");
let neptune = new Pet("fish", "Neptune");
console.log(`I am a ${pudding.animal}. My name is ${pudding.name}.`);
pudding.sleep(); // I am sleeping
pudding.wake();  // I am awake

console.log(`I am a ${neptune.animal}. My name is ${neptune.name}.`);
neptune.sleep(); // I am sleeping
neptune.wake();  // I am awake
```

### [The Class Syntactic Sugar](https://launchschool.com/lessons/24a4613a/assignments/9892763f)

- yup

### [Practice Problems: Classes](https://launchschool.com/lessons/24a4613a/assignments/991c89d6)

Simple! And fun!

### [Which Pattern Should I Use?](https://launchschool.com/lessons/24a4613a/assignments/7038e6ad)

- classes

### [More Methods on the Object Constructor](https://launchschool.com/lessons/24a4613a/assignments/8db4bc31)

- I didn't get the exercises right.
- LS answer:

```javascript
function newPerson(name) {
  return Object.defineProperties({ name: name }, {
    log: {
      value() {
        console.log(this.name);
      },
      writable: false
    },
  });
}
```
#### Object.freeze

- because the array and object are compound objects, .freeze only works on property values that are not objects. It freezes he reference, not the object.
### [Modules](https://launchschool.com/lessons/24a4613a/assignments/be1ff8b5)

#### [gist](https://launchschool.com/gists/e7d0531f)

- Two module systems:
  - CommonJS modules, also known as Node modules.
  - JS modules, also known as "ES modules" and "ECMAScript modules."

##### Benefits of Modules
  - Avoid large sprawling programs that have the following disadvantages:
    - hard to understand
    - more tightly coupled components (as more changes are made the different parts become more intertwined and ripples effects are less controlable)
    - As they grow they move away from their simple, easy-to-follow, purposeful origin.
    - Programming often involves working on multiple parts at once and in such a program this requires lots of jumping around.
    - If there are multiple devs working on this one file then there can be problems when trying to combine the work.
    - Encapsulation is a bothersome addition if everything is in the same file.
  - The solution to all of the above is to seperate your code into multiple files, called 'modules':
    - Each module focuses on different parts of the problem
    - A team of devs can work on it without confllicting
    - You don't need to chase down function calls
    - Different parts tend not to become entangled as they grow
    - Helps with private data / encapsulation because modules are private by default.
    - You can easily use a module elsewhere without having to disentangle it from the program.

##### CommonJS Modules

- Node supports modules. That's how we can `require` other files
  - `
- Not all flavors of JavaScript support CommonJS modules, notably the browswer doesn't (because CommonJS modules are loaded synchronously, not async -> more on that later) (syncchronous takes too long)(unless you use a transpiler)
- 

###### Creating CommonJS Modules

```javascript
function logIt(string) {
  console.log(string);
}

module.exports = logIt;
```

- You can export multiple things at once :

```javascript
let prefix = ">> ";

function logIt(string) {
  console.log(`${prefix}${string}`);
}

function setPrefix(newPrefix) {
  prefix = newPrefix;
}

module.exports = {
  logIt,
  setPrefix,
};
```

###### CommonJS Variables

- module: an object that represents the current module :
  
```
 
{
  id: '.',
  path: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules',
  exports: {},
  filename: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/03_node_variables.js',
  loaded: false,
  children: [],
  paths: [
    '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/node_modules',
    '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/node_modules',
    '/Users/sandyboy/Desktop/JS225_OOJ/node_modules',
    '/Users/sandyboy/Desktop/node_modules',
    '/Users/sandyboy/node_modules',
    '/Users/node_modules',
    '/node_modules'
  ],
  [Symbol(kIsMainSymbol)]: true,
  [Symbol(kIsCachedByESMLoader)]: false,
  [Symbol(kURL)]: undefined,
  [Symbol(kFormat)]: undefined,
  [Symbol(kIsExecuting)]: true
}
```

- exports: the name(s) exported by the module (same as module.exports):

```javascript
{}
```

- require(moduleName): the function that loads a module:

```javascript
[Function: require] {
  resolve: [Function: resolve] { paths: [Function: paths] },
  main: {
    id: '.',
    path: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules',
    exports: {},
    filename: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/03_node_variables.js',
    loaded: false,
    children: [],
    paths: [
      '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/node_modules',
      '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/node_modules',
      '/Users/sandyboy/Desktop/JS225_OOJ/node_modules',
      '/Users/sandyboy/Desktop/node_modules',
      '/Users/sandyboy/node_modules',
      '/Users/node_modules',
      '/node_modules'
    ],
    [Symbol(kIsMainSymbol)]: true,
    [Symbol(kIsCachedByESMLoader)]: false,
    [Symbol(kURL)]: undefined,
    [Symbol(kFormat)]: undefined,
    [Symbol(kIsExecuting)]: true
  },
  extensions: [Object: null prototype] {
    '.js': [Function (anonymous)],
    '.json': [Function (anonymous)],
    '.node': [Function (anonymous)]
  },
  cache: [Object: null prototype] {
    '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/03_node_variables.js': {
      id: '.',
      path: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules',
      exports: {},
      filename: '/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/03_node_variables.js',
      loaded: false,
      children: [],
      paths: [Array],
      [Symbol(kIsMainSymbol)]: true,
      [Symbol(kIsCachedByESMLoader)]: false,
      [Symbol(kURL)]: undefined,
      [Symbol(kFormat)]: undefined,
      [Symbol(kIsExecuting)]: true
    }
  }
}
```

- __dirname: the absolute pathname of the directory that contains the module:

`/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules`

- __filename: the absolute pathname of the file that contains the module:

`/Users/sandyboy/Desktop/JS225_OOJ/05_object_creation_patterns/19_modules/03_node_variables.js`

##### JS Modules

###### Some History

-  RequireJS and Browserify
-  Babel and Webpack to support older browsers

###### Using JS Modules

This part is about how to import and export moduels on the browser and I'm going to skip it for now.

### [Douglas Crockford Lecture - JavaScript: the Good Parts](https://launchschool.com/lessons/24a4613a/assignments/a02e7ce6)

- I will need to watch this when Youtube isn't blocked

### [Summary](https://launchschool.com/lessons/24a4613a/assignments/bd49b355)

- Yes

###### tangent: open source contributions

- https://westonludeke.medium.com/my-first-open-source-contribution-ff63fadc4a94
- https://launchschool.com/posts/ea9a6854
- https://www.firsttimersonly.com

### [Quiz](https://launchschool.com/lessons/24a4613a/assignments/17ccc38c)

- 6/7

## [6 Projects](https://launchschool.com/lessons/303f0e4f/home)

### [Introduction](https://launchschool.com/lessons/303f0e4f/assignments/f5610e4f)

- call-back to RB120

### [Tic-tac-toe](https://launchschool.com/lessons/303f0e4f/assignments/f6bb76f9)

- [RB120 link](https://launchschool.com/lessons/97babc46/assignments/7dcb53f1)

Minimum accaptable:

```javascript
const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares)
    let r = allSquares.filter(([_, square]) => square.isUnmarked())
    // console.log(`r.length is ${r.length}`)
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0
  }

  someoneWon() {
    // console.log(`this.detectWinner() is : ${this.detectWinner()}`)
    // console.log(`which, with !! in front is : ${!!this.detectWinner()}`)
    return !!this.detectWinner();
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }
}

class Square {
  initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === this.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves() {
    let unmarkedKeys = this.board.unmarkedKeys();
    let chosenSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  playAgain() {
    let answer;
    while (!answer) {
      answer = readlineSync.question("Would you like to play again? (y/n)")
      if (!['y','n'].includes(answer.toLowerCase())) {
        console.log("Sorry, answer must be 'y' or 'n'")
        answer = false;
      }
    }
    return answer.toLowerCase() === 'y'
  }

  refresh() {
    console.clear();
  }

  postPlayProtocol() {
    this.displayResult();
    if (this.playAgain()) {
      this.refresh()
      this.board = new Board;
      this.play();
    } else {
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    this.displayBoard();
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        this.computerMoves()
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol();
        }
      }
    }
    this.postPlayProtocol()
  }
}

let game = new TTTGame;
game.play();
```

- with computer strategy:

```javascript
/*


If neither player can win with a single play and the center square is empty, play the center square.
If none of the above conditions apply, pick a square at random.

*/

const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares);
    let r = allSquares.filter(([_, square]) => square.isUnmarked());
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0;
  }

  someoneWon() {
    return !!this.detectWinner();
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }

  victoryIfThisOneSquareFilledBy(player = this.human) {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      let emptySquares = line.filter((num) => this.squares[num].marker === Square.initialMarker);
      let filledSquares = line.filter((num) => this.squares[num].marker === player.marker);
      if (emptySquares.length === 1 && filledSquares.length === 2) { 
        // let playerName = player.marker === 'X' ? 'Human' : 'Computer';
        // console.log(`${playerName} will win if they fill square ${emptySquares[0]}`);
        return emptySquares[0];
      }
    }
  }
}

class Square {
  static initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === Square.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    // this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      // console.log(`line205: this.board.unmarkedKeys() is ${this.board.unmarkedKeys()}`)
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves(targetSquare) {
    let unmarkedKeys = this.board.unmarkedKeys();
    let randomSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    let chosenSquare = targetSquare ? targetSquare : randomSquare;
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  playAgain() {
    let answer;
    while (!answer) {
      answer = readlineSync.question("Would you like to play again? (y/n)")
      if (!['y','n'].includes(answer.toLowerCase())) {
        console.log("Sorry, answer must be 'y' or 'n'")
        answer = false;
      }
    }
    return answer.toLowerCase() === 'y'
  }

  refresh() {
    console.clear();
  }

  postPlayProtocol() {
    this.displayResult();
    if (this.playAgain()) {
      this.refresh()
      this.board = new Board;
      this.play();
    } else {
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    this.displayBoard();
    // console.log(`line208: ${this.board.victoryIfThisOneSquareFilled()}`);
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      this.board.victoryIfThisOneSquareFilledBy(this.human)
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        let nextComputerMove = this.board.victoryIfThisOneSquareFilledBy(this.computer)
        let nextHumanMove = this.board.victoryIfThisOneSquareFilledBy(this.human)
//  If the computer can win with a single play, make that play.
        if (nextComputerMove) {
          this.computerMoves(nextComputerMove);
//  If the computer can't win with a single play, but the human can, then try to block that play.
        } else if (nextHumanMove) {
          this.computerMoves(nextHumanMove);
//  If neither player can win with a single play and the center square is empty, play the center square.
        } else if (this.board.unmarkedKeys().includes(5)) {
          this.computerMoves(5);
//  If none of the above conditions apply, pick a square at random.
        } else {
          this.computerMoves()
        }
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol();
        }
      }
    }
    this.postPlayProtocol()
  }
}

let game = new TTTGame;
game.play();
```

- Best of 3:

```javascript
/*


If neither player can win with a single play and the center square is empty, play the center square.
If none of the above conditions apply, pick a square at random.

*/

const readlineSync = require('readline-sync');

class Board {
  winningLines = [[1, 2, 3], [4, 5, 6], [7, 8, 9],
                  [1, 4, 7], [2, 5, 8], [3, 6, 9], 
                  [1, 5, 9], [3, 5, 7]];

  constructor() {
    this.squares = {};
    for (let i = 1; i < 10; i++) {
      this.squares[i] = new Square(' ');
    }
  }

  getSquareAt(key) {
    return this.squares[key].marker;
  }

  setSquareAt(key, marker) {
    this.squares[key].marker = marker;
  }

  unmarkedKeys() {
    let allSquares = Object.entries(this.squares);
    let r = allSquares.filter(([_, square]) => square.isUnmarked());
    return r.map((elem) => elem[0]);
  }

  isFull() {
    return this.unmarkedKeys().length === 0;
  }

  someoneWon() {
    return this.detectWinner()
  }

  detectWinner() {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      if (this.squares[line[0]].marker === TTTGame.humanMarker &&
          this.squares[line[1]].marker === TTTGame.humanMarker &&
          this.squares[line[2]].marker === TTTGame.humanMarker) {
            return TTTGame.humanMarker;
        } else if (
          this.squares[line[0]].marker === TTTGame.computerMarker &&
          this.squares[line[1]].marker === TTTGame.computerMarker &&
          this.squares[line[2]].marker === TTTGame.computerMarker) {
            return TTTGame.computerMarker;
        }
    }
  }

  victoryIfThisOneSquareFilledBy(player = this.human) {
    for (let i = 0; i < this.winningLines.length; i++) {
      let line = this.winningLines[i];
      let emptySquares = line.filter((num) => this.squares[num].marker === Square.initialMarker);
      let filledSquares = line.filter((num) => this.squares[num].marker === player.marker);
      if (emptySquares.length === 1 && filledSquares.length === 2) { 
        // let playerName = player.marker === 'X' ? 'Human' : 'Computer';
        // console.log(`${playerName} will win if they fill square ${emptySquares[0]}`);
        return emptySquares[0];
      }
    }
  }
}

class Square {
  static initialMarker = " ";
  
  constructor(marker) {
    this.marker = marker;
  }

  isUnmarked() {
    return this.marker === Square.initialMarker;
  }
}

class Player {
  constructor(marker) {
    this.marker = marker;
    this.winCount = 0;
  }
}

class TTTGame {
  static humanMarker = 'X';
  static computerMarker = 'O';

  constructor() {
    this.board = new Board;
    this.human = new Player(TTTGame.humanMarker);
    this.computer = new Player(TTTGame.computerMarker);
  }

  displayWelcomeMessage() {
    console.log("Welcome to Tic Tac Toe!\r");
  }

  displayGoodbyeMessage() {
    console.log('Thanks for playing Tic Tac Toe! Goodbye!\r');
  }

  displayBoard() {
    // this.refresh();
    console.log( ``);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(1)}  |  ${this.board.getSquareAt(2)}  |  ${this.board.getSquareAt(3)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(4)}  |  ${this.board.getSquareAt(5)}  |  ${this.board.getSquareAt(6)}`);
    console.log( `     |     |`);
    console.log( `-----+-----+-----`);
    console.log( `     |     |`);
    console.log( `  ${this.board.getSquareAt(7)}  |   ${this.board.getSquareAt(8)} |  ${this.board.getSquareAt(9)}`);
    console.log( `     |     |`);
    console.log( ``);
  }

  humanMoves() {
    console.log(`Choose a square (${this.board.unmarkedKeys().join(', ')}): `);
    let square;
    while (!square) {
      let choice = readlineSync.question('which square do you choose? (1- 9)\n');
      // console.log(`line205: this.board.unmarkedKeys() is ${this.board.unmarkedKeys()}`)
      if (!this.board.unmarkedKeys().includes(choice))
        console.log(`invalid choice, try again`);
      else {
        square = choice;
      }
    }
    this.board.setSquareAt(square, this.human.marker)
  }

  computerMoves(targetSquare) {
    let unmarkedKeys = this.board.unmarkedKeys();
    let randomSquare = unmarkedKeys[Math.floor(Math.random() * unmarkedKeys.length)];
    let chosenSquare = targetSquare ? targetSquare : randomSquare;
    this.board.setSquareAt(chosenSquare, TTTGame.computerMarker);
  }

  boardFull() {
    return this.board.unmarkedKeys().length === 0;
  }

  displayResult() {
    this.displayBoard();
    let potentialWinner = this.board.detectWinner();
    if ( potentialWinner === 'O') {
      console.log(`Computer wins`)
    } else if (potentialWinner === 'X') {
      console.log(`You win`)
    } else if (this.boardFull()) {
      console.log("It's a draw!")
    }
  }

  refresh() {
    console.clear();
  }

  thriceWinner() {
    if (this.human.winCount === 3) {
      return 'human';
    } else if (this.computer.winCount === 3) {
      return 'computer';
    }
  }

  incrementWinCount(marker) {
    if (marker === TTTGame.humanMarker) {
      this.human.winCount += 1;
    } else if (marker === TTTGame.computerMarker) {
      this.computer.winCount += 1
    }
  }

  checkForWinner() {
    if (this.human.winCount === 3) {
      return "human";
    } else if (this.computer.winCount === 3) {
      return "computer";
    }
  }

  displayScore() {
    console.log(`Human: ${this.human.winCount} | Computer: ${this.computer.winCount}`)
  }

  postPlayProtocol(marker) {
    this.incrementWinCount(marker);
    this.displayResult();
    this.displayScore();
    let thriceWinner = this.thriceWinner();
    if (!thriceWinner) {
      // this.refresh()
      this.board = new Board;
      this.play();
    } else {
      console.log(`${thriceWinner} has won thrice! Game over`);
      this.displayGoodbyeMessage();
    }
  }

  play() {
    this.displayWelcomeMessage();
    // this.displayBoard();
    while (!this.board.someoneWon() || !this.boardFull()) {
      this.displayBoard();
      this.humanMoves()
      if (this.board.someoneWon() || this.boardFull()) {
        return this.postPlayProtocol();
      } else {
        let nextComputerMove = this.board.victoryIfThisOneSquareFilledBy(this.computer)
        let nextHumanMove = this.board.victoryIfThisOneSquareFilledBy(this.human)
        if (nextComputerMove) {
          this.computerMoves(nextComputerMove);
        } else if (nextHumanMove) {
          this.computerMoves(nextHumanMove);
        } else if (this.board.unmarkedKeys().includes(5)) {
          this.computerMoves(5);
        } else {
          this.computerMoves()
        }
        if (this.board.someoneWon() || this.boardFull()) {
          return this.postPlayProtocol(this.board.someoneWon());
        }
      }
    }
    this.postPlayProtocol(this.board.someoneWon());
  }
}

let game = new TTTGame;
game.play();
```

### [Twenty-one](https://launchschool.com/lessons/303f0e4f/assignments/235718a8)

- Fiddly. I definitely lost myself in the weeds. Next time I will make a more comprehensive plan about what objects get passed where, what their responsibilities are etc. Have a piece of paper where I can draw objects and their relationships

# Assessment Prep

- I plan to take the assessment at the end of April, which is in 22 days (Wednesday 30th)
  - could it be even sooner? Part 1: 25th, Part2: 30th?
- Steps:
  - create comprehensive document (This page) which has my notes + hyper-links to the parts of the course that reference the relevant material.
  - Write a list of expected questions with answers
    - + topics I'm shaky on.
  - Finish
    - JS225 exercises
    - JS210 exercises where I can't find that I've done them
    - Read discussion board for JS229
    - Read these 4 articles
      - JavaScript Weekly: Making Sense of Closures (read 8.4.25)
      - JavaScript Weekly: Understanding Links on the Object Prototype Chain
      - JavaScript Weekly: An Introduction to First-Class Functions
      - JavaScript Weekly: What in the World is this?!

  - Be ruthless about getting excellent sleep. (no alcohol)
  - Maintain art. I think It's necessary for my equilibrium.
  - Start working afternoons?
  - Cancel:
    -  AM's wedding?
    -  Beach-rave?

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

### My progress

|| first pass | second pass| third pass
|:--|:--|:--|:--|
|Start| 11.3.25 | 5.3.25 |
|L1: About this course| 11.3.25 ||
|L2: Objects|13.3.25||
|L3: Function Contexts and Objects|15.3.25|||
|L4: Closures and function scope| 17.3.25||
|L5: Object Creation Patterns |31.3.25 ||
|L6: Object Creation Patterns |4.4.25||

#### quizes:

|| first | second | third
|:--|:--|:--|:--|
|L2: Objects|13.3.25 - 7/8 (88%)||
|L3: Function Contexts and Objects|15.3.25 - 6/9 (67%)|||
|L4: Closures and function scope| 17.3.25 - 6/7 (86%)||
|L5: Object Creation Patterns |31.3.25 - 6/7 (86%)||
