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


### [Practice Problems: What is this? (1)](https://launchschool.com/lessons/c9200ad2/assignments/82f593ef)

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
