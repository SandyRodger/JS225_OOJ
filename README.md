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



### 8	Practice Problems: Mutating Objects
### 9	Collaborator Objects
### 10	Functions as Object Factories
### 11	Practice Problems: Functions as Object Factories
### 12	Object Orientation
### 13	Practice Problems: Object Orientation
### 14	Summary

## 3 Function Contexts and Objects	
## 4 Closures and Function Scope
## 5 Object Creation Patterns
## 6 Projects
