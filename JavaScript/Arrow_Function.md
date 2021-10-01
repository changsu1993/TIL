# 1. Function (함수)

## Function

- fundamental building block in the program
- subprogram can be used multiple times
- performs a task or calculates a value
  <br><br>

## Function declaration

function name(param1, param2) {body... return;}

one function === one thing

naming: doSomething, command, verb

e.g. createCardAndPoint -> createCard, createPoint

function is object in JS

```javascript
function printHello() {
  console.log('Hello');
}
printHello();

function log(message) {
  console.log(message);
}
log('Hello');
```

<br>

## Parameters

premitive parameters: passed by value <br>
object parameters: passed by reference

```javascript
function changeText(a) {
  a.text = 'Hello';
}
const b = { text: 'world' };
changeText(b);
console.log(b); // {text: 'Hello'}
```

<br>

## Default parameters (added in ES6)

```javascript
function showMessage(message, from = 'unknown') {
  console.log(`${message} by ${from}`);
}
showMessage('Hi!'); // Hi! by unknown
```

<br>

## Rest parameters (added in ES6)

```javascript
function printAll(...args) {
  for (let i = 0; i < args.length; i++) {
    console.log(args[i]);
  }
}
printAll('Hi', 'Hello', 'World');
// Hi
// Hello
// World
```

<br>

## Function expression

a function declaration can be called earlier than it is defiend. (hoisted) <br>
a function expression is created when the execution reaches it. <br>

```javascript
const print = function () {
  // anonymous function
  console.log('print');
};
print(); // print
const printAgain = print;
printAgain(); // print
```

<br>

```javascript
// Callback function using function expression

function randomQuiz(answer, printYes, printNo) {
  if (answer === 'Thank you') {
    printYes();
  } else {
    printNo();
  }
}
// anonymous function
const printYes = function () {
  console.log('yes');
};

// named function
// better debugging in debugger's stack traces
// recursions
const printNo = function print() {
  console.log('no');
};

randomQuiz('wrong', printYes, printNo); // no!
randomQuiz('Thank you', printYes, printNo); // yes!
```

<br>

## Arrow function

```javascript
// Arrow function
// always anonymous
const simplePrint = function () {
  console.log('simplePrint');
};

const simplePrint = () => console.log('simplePrint');

const add = (a, b) => a + b;
```

<br>

## IIFE

Immediately Invoked Function Expression

```javascript
(function hello() {
  console.log('IIFE');
})();
```
