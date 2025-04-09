**Most/all of these discussion posts refer to the section of JS229 that comes after the written assessment**

## [Testing Template](https://launchschool.com/posts/bbf8d609)

- This is a practice project required after one has completed the written assessment.

```javascript
var $ol = document.querySelector("ol");

function outputResult(message) {
  var $li = document.createElement("li");
  $li.innerText = message;
  $ol.appendChild($li);
  return $li;
}

function test(message, assertion) {
  var $msg = outputResult(message),
      passed = false;

  try {
    passed = assertion();
  }
  catch (e) {
    passed = false;
  }
  $msg.setAttribute("class", passed ? "pass" : "fail");
}
```

## [take home project prep](https://launchschool.com/posts/04f33dd1)

- similar to ['mini inventory management system'](https://launchschool.com/exercises/d6d3971a)

## [ESLint in 'take home project'](https://launchschool.com/posts/2fd54203)

- would be good to use. Soundslike Rubocop

## [Chrome Developer Tool - How to use it for testing?](https://launchschool.com/posts/748ff1d5)

- "the JavaScript Utility Library which serves as a practice project for the take home assessment" ? I'll keep an eye out. It rings a bell.

## [Using jest to import classes](https://launchschool.com/posts/c00ce5a9)

```
npm list jest --save-dev
touch jest.config.js
npx jest foo.test.js
```

##
