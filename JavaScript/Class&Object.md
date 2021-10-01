# 1. Class & Object

## Class

- template
- declare once
- no data in

(introduced in ES6, syntactical sugar over prototype-based inheritance)

클래스 자체에는 데이터가 들어있지 않고, 템플릿만 정의하고 선언한다.
<br><br>

## Object

- instance of a class
- created many times
- data in

클래스를 이용해 새로운 인스턴스를 생성하면 object가 된다.

---

<br>

## Class declarations

```javascript
class Person {
  //constructor
  constructor(name, age) {
    //fields
    this.name = name;
    this.age = age;
  }

  // methods
  speak() {
    console.log(`${this.name}: hello!`);
  }
}

// Object 생성
const petter = new Person('petter', 20);
console.log(petter.name); // petter
console.log(petter.age); // 20
petter.speak(); // petter: hello!
```

<br>

## Getter and Setter

```javascript
class User {
  constructor(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
  }

  get age() {
    return this._age;
  }

  set age(value) {
    // if (value < 0) {
    //   throw Error('age can not be negative')l
    // }
    this._age = value < 0 ? 0 : value;
  }
}

const user1 = new User('steve', 'Job', -1);
console.log(user1.age); // -1
```

<br>

## Public & Private

```javascript
// Fields (public, private)
class Experiment {
  publicField = 2;
  #privateField = 0;
}
const experiment = new Experiment();
console.log(experiment.publicField); // 2
console.log(experiment.privateField); // undefined
```

<br>

## Static

```javascript
// Static properties and methods

class Article() {
  static publisher = 'Petter';
  constructor(articleNumber) {
    this.articleNumber = articleNumber;
  }

  static printPublisher() {
    console.log(Article.publisher); // undefined
  }
}
const article1 = new Article(1);
const article2 = new Article(2);
console.log(article1.publisher); // undefined
// static은 object마다 할당되어지는 것이 아닌 class 자체에 붙어있다.
console.log(Article.publisher); // petter
Article.printPublisher(); // petter
```

<br>

## Inheritance

```javascript
// a way for one class to extend another class.
class Shape {
  constructor(width, height, color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }

  draw() {
    console.log(`drawing ${this.color} color of`);
  }

  getArea() {
    return width * this.height;
  }
}

class Rectangle extends Shape {}
class Triangle extends Shape {
  draw() {
    super.draw(); // drawing red color
    console.log('🔺'); // 🔺
  }
  getArea() {
    // Overriding
    return (this.width * this.height) / 2;
  }
}

const rectangle = new Rectangle(20, 20, 'blue');
rectangle.draw(); // drawing blue color of
console.log(rectangle.getArea()); // 400
const triangle = new Triangle(20, 20, 'red');
triangle.draw(); // drawing red color of
console.log(triangle.getArea()); // 200
```

<br>

## InstanceOf

```javascript
// Class checking: instanceOf
console.log(rectangle instanceof Rectangle);
// true
console.log(triangle instanceof Rectangle);
// false
console.log(triangle instanceof Triangle);
// true
console.log(triangle instanceof Shape);
// true
console.log(triangle instanceof Object);
// true
```
