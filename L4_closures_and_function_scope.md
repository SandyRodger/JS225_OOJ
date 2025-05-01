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
##### Q: How does one create and use private data?

A:
closures:
function createAccount() {
  let balance = 100;
  return {
    deposit(n) {
      balance += n;
      console.log(`new balance is ${balance}`);
    },
    withdraw(n) {
      balance -= n;
      console.log(`new balance is ${balance}`);
    },
    displayBalance() {
      console.log(`balance is ${balance}`);
    }
  }
}

let myAccount = createAccount();
myAccount.deposit(200); // new balance is 300
myAccount.withdraw(30); // new balance is 270
myAccount.displayBalance(); // balance is 270
console.log(myAccount.balance) // undefined
private data in classes:
class Account {
  #balance = 100;

  constructor(accountHolder) {
    this.accountHolder = accountHolder;
    this.interestPercent = 4;
  }

  #displayBalancePrivate() {
    console.log(this.#balance)
  };
  displayBalancePublic() {
    this.#displayBalancePrivate()
  };
}

let myAccount = new Account('Alex')
myAccount.displayBalancePublic() // 100
// myAccount.#displayBalancePrivate() // SyntaxError
// console.log(myAccount.#balance) // SyntaxError
IIFEs:
let myAccount = (function() {
  let balance = 100;
  return {
    deposit(n) {
      balance += n;
      console.log(`new balance is ${balance}`);
    },
    withdraw(n) {
      balance -= n;
      console.log(`new balance is ${balance}`);
    },
    displayBalance() {
      console.log(`balance is ${balance}`);
    }
  }
})()

myAccount.displayBalance(); // balance is 100
myAccount.deposit(200); // new balance is 300
myAccount.withdraw(2); // new balance is 298
myAccount.displayBalance(); // balance is 298
console.log(myAccount.balance) // undefined
Private data is crucial in Javascript for protecting data from unintended modification and for data-encapsulation and  security.

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
