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
