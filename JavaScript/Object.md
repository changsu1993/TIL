# 1. Object

one of the JavaScript's data types. <br>
a collection of related data and/or functionality. <br>
Nearly all objects in JavaScript are instances of Object. <br>
object = { key : value };

```javascript
const name = 'petter';
const age = 20;
print(name, age);
function print(name, age) {
  console.log(name);
  console.log(age);
}

// Object
// Literals and properties
const obj1 = {}; // 'object literal' syntax
const obj2 = new Object(); // 'object constructor' syntax

const petter = { name: 'petter', age: 20 };
function objprint(person) {
  console.log(person.name);
  console.log(person.age);
}
print(petter);

// with JavaScript magic (dynamically typed language)
// can add properties later
petter.hasJob = true;
console.log(petter.hasJob);

// can delete properties later
delete petter.hasJob;

// object['key']
// Computed properties
// key should be always string
console.log(petter.name);
console.log(petter['name']);
petter['hasJob'] = true;
console.log(petter.hasJob);

function printValue(obj, key) {
  console.log(obj[key]);
}
printValue(petter, 'name');
printValue(petter, 'age');

// Property value shorthand
const person1 = { name: 'bob', age: 2 };
const person2 = { name: 'steve', age: 3 };
const person3 = { name: 'dave', age: 4 };
const person4 = new Person('petter', 20);
console.log(person4);

// Constuctor Function
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// in operator: property existence check (key in obj)
console.log('name' in petter);
console.log('age' in petter);

// for..in vs for..of
// for (key in obj)
for (key in petter) {
  console.log(key); // name age hasJob
}

// for (value of iterable)
const array = [1, 2, 3, 4];
for (value of array) {
  console.log(value); // 1 2 3 4
}

// Fun cloning
// Object.assian(dest, [obj1, obj2, obj3...])
const user = { name: 'petter', age: 20 };
const user2 = user;
user2.name = 'coder';
console.log(user); // { name: 'coder', age: 20 }

// old way
const user3 = {};
for (key in user) {
  user3[key] = user[key];
}
console.log(user3); // { name: 'coder', age: 20 }

const user4 = {};
Object.assign(user4, user);
console.log(user4); // { name: 'coder', age: 20 }
// or
const user4 = Object.assign({}, user);
```
