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
### [Constructor Pattern](https://launchschool.com/lessons/24a4613a/assignments/c659f8e4)



### [Objects and Prototypes](https://launchschool.com/lessons/24a4613a/assignments/da0992e3)

#### The __proto__ Property

- "dunder"

#### Prototype Chain and the Object.prototype Object



### [Prototypal Inheritance and Behavior Delegation](https://launchschool.com/lessons/24a4613a/assignments/7143264c)

#### Overriding Default Behavior
#### Object.getOwnPropertyNames and object.hasOwnProperty
#### Methods on Object.prototype

### [Practice Problems: Prototypes and Prototypal Inheritance](https://launchschool.com/lessons/24a4613a/assignments/b158be5a)



### [Function Prototypes and Object Prototypes](https://launchschool.com/lessons/24a4613a/assignments/441a520a)



### [Constructors, Prototypes, and the Prototype Chain](https://launchschool.com/lessons/24a4613a/assignments/5de6e5a0)



### Practice Problems: Constructor Functions and Prototypes (1)
### Practice Problems: Constructor Functions and Prototypes (2)
### Static and Instance Properties and Methods
### The Pseudo-classical Pattern and the OLOO Pattern
### The Class Syntactic Sugar
### Practice Problems: Classes
### Which Pattern Should I Use?
### More Methods on the Object Constructor
### Modules
### Douglas Crockford Lecture - JavaScript: the Good Parts
### Summary

## 6 Projects

#### quizes:

|| first | second | third
|:--|:--|:--|:--|
|L2: Objects|13.3.25 - 7/8 (88%)||
|L3: Function Contexts and Objects|15.3.25 - 6/9 (67%)|||
|L4: Closures and function scope| 17.3.25 - 6/7 (86%)||
|L5: Object Creation Patterns |||
