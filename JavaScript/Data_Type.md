# 1. Data Type(데이터 타입)

자바스크립트 데이터 타입은 기본 타입(Primitive Type)과 참조 타입(Object/Reference Type)이 있다.

**기본 타입**

- 문자열(string)
- 숫자(number)
- boolean
- undefined
- null
- symbol

**참조 타입**

- 객체
- 함수

(정규표현식, 배열등 원시 타입을 제외한 나머지 값들은 객체로 볼 수 있다.)
<br><br>

## Primitive Type

**문자열(String)** <br>
16비트 유니코드 문자셋(UTF-16)으로 구성되어 있고, 작은따옴표, 큰따옴표, 템플릿 리터럴으로 문자열을 할당할 수 있다.<br>
템플릿 리터럴(template literal)은 ES6에서 도입되었다.

```javascript
let str = 'hello world';
let str = 'hello world';
let str = `hello world`;
let str = `hello 
world ${test} `;
// 템플릿 리터럴을 쓸 경우 공백, 줄바꿈 등을 쓸 때 편하고 문자열 안에 ${}를 써서 변수를 편하게 쓸 수 있다.
```

<br>

**숫자(Number)** <br>
64비트 부동소수점 형식으로, 숫자를 실수로 처리한다.

```javascript
let a = 11;
let b = 42 / 0; // +Infinity
let c = 42 / -0; // -Infinity
let d = 1 * 'str'; // NaN
```

<br>

**Boolean** <br>
Boolean 값은 논리적 참, 거짓을 나타내는 true와 false가 있다.

**true로 변환되는 값**

- 문자열: 비어있지 않은 문자열
- 숫자: 0이 아닌 모든 숫자
- 객체: 모든 객체

**false로 변환되는 값**

- 문자열: ''(빈 문자열)
- 숫자: 0, NaN
- 객체: null
- undefined

<br>

**Undefined** <br>
값이 할당되지 않았을 때, 자바스크립트 엔진이 타입과 값을 모두 undefined로 초기화한다.

<br>

**Null** <br>
의도적으로 빈 값을 주기위해 할당하는 값 (타입은 null이 아닌 object이므로 주의해야 한다.)

<br>

**Symbol** <br>
ES6에서 새로 생긴 데이터 타입으로, 변경불가능한 유일한 값을 생성할 때 사용하며, 값 자체가 확인이 불가하여 외부로 노출되지 않는다.

<br>

## Object/Reference Type

자바스크립트는 객체 기반의 스크립트 언어로써 자바스크립트를 이루고 있는 거의 모든 것이 객체이다. 객체는 데이터와 그 데이터에 관련한 동작을 모두 포함할 수 있는 개념적 존재로써 Property와 Method를 포함할 수 있는 독립적 주체이다. 객체는 참조에 의한 전달(pass-by-reference)방식으로 전달된다.
