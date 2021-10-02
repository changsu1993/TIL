# 1. Array & APIs (배열)

```javascript
// 1. Declaration
const arr1 = new Array();
const arr2 = [1, 2];

// 2. Index position
const fruits = ['apple', 'banana'];
console.log(fruits); // ['apple', 'banana']
console.log(fruits.length);
2;
console.log(frutis[0]); // apple

// 3. Looping over an array
// print all fruits

// a. for
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}

// b. for of
for (let fruit of fruits) {
  console.log(fruit); //
}

// c. forEach
fruits.forEach((fruit) => console.log(fruit);

// d. Addtion, deletion, copy
// push: add an item to the end
fruits.push('mango', 'orange');
console.log(fruits); // ['apple', 'banana', 'mango', 'orange']

// pop: remove an item from the end
fruits.pop();
console.log(fruits); // ['apple', 'banana', 'mango']

// unshift: add an item to the benigging
fruits.unshift('mango', 'orange');
console.log(fruits); // ['mango', 'orange', 'apple', 'banana']

// shift: remove an item from the benigging
fruits.shift();
console.log(fruits); // ['orange', 'apple', 'banana']

// shift, unshift are slower than pop, push

// splice: remove an item by index position
fruits.push('mango', 'orange');
console.log(fruits); // ['apple', 'banana', 'mango', 'orange']
fruits.splice(1, 1); // ['apple', 'mango', 'orange']
fruits.splice(1, 1, 'a', 'b'); // ['apple', 'a', 'b', 'mango', 'orange']

// combine two arrays
const fruits2 = ['melon', 'strawberry'];
const newFruits = fruits.concat(fruits2);
console.log(newFruits); // ['apple', 'banana', 'melon', 'strawberry']

// e. Searching
// find the index
console.log(newFruits);
console.log(newFruits.indexOf('apple')); // 0
console.log(newFruits.includes('apple')); // true
fruits.push('apple');
console.log(newFruits.lastIndexOf('apple')); // 4
```
