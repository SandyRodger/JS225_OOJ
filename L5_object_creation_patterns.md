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

(I had already seen this)

- Good parts:
  - Lambda
  - Dynamic Objects
  - Loose typing
  - Object Literals.
- Inheritance is object oriented code re-use.
- Two-schools:
  - Classical
  - Prototypal (this can do classical, can be other way round though)
- Prototypal inheritance -> each object contains only what differentiates it from the object it inherits
- JSLint: [42:40]
- Unlearning falsehoods is much harder than learning thuths.
- "Object hardening" (47:40), are objects too dynamic?
- "new strict mode" (2008) The web has found usage for all of the bad parts of the language, therefore strict mode is optional.
- [52:00] strict mode
  - strict mode: does it change behaviour?

### [Summary](https://launchschool.com/lessons/24a4613a/assignments/bd49b355)

- Yes

###### tangent: open source contributions

- https://westonludeke.medium.com/my-first-open-source-contribution-ff63fadc4a94
- https://launchschool.com/posts/ea9a6854
- https://www.firsttimersonly.com

### [Quiz](https://launchschool.com/lessons/24a4613a/assignments/17ccc38c)

- 6/7
