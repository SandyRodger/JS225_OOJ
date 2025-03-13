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



### Dealing with Context Loss (3)
###	Practice Problems: Dealing with Context Loss
###	Summary: The this Keyword in JavaScript
###	Practice Problems: What is this? (1)
###	Practice Problems: What is this? (2)
###	Summary
###	Quiz


## 4 Closures and Function Scope
## 5 Object Creation Patterns
## 6 Projects
