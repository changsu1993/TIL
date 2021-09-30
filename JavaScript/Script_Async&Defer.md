# 1. Script Async와 Defer

```javascript
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
    <script src="main.js"></script>
  </head>
  <body></body>
</html>
```

기본적으로 사용자가 HTML 파일을 다운로드 하였을 때, 브라우저가 한 줄씩 분석하고 이해한 것을 CSS와 병합해서 DOM요소로 변환하게 된다.

\<head>태그 안에 단순히 js를 포함할 경우, HTML을 순서대로 읽어나가다가 자바스크립트 파일을 읽으면 HTML 읽어나가는 것을 잠시 멈추고 필요한 자바스크립트 파일을 서버에서 다운로드하여 실행 후 진행된다.

만약 인터넷이 느리고 작성한 js파일의 크기가 크다면 사용자가 웹사이트를 보는 데까지 많은 시간이 소요될 수 있다는 단점이 있다.
<br><br>

---

<br>

```javascript
<html lang='ko'>
  <head>
    <meta charset='UTF-8' />
    <title>Document</title>
  </head>
  <body>
    <div></div>
    <script src='main.js'></script>
  </body>
</html>
```

\<body>태그 끝부분에 script를 추가하는 방법도 있다.

브라우저가 HTML을 먼저 다운로드 한 후에 스크립트를 다운로드 하기 때문에 사용자가 기본적인 HTML의 콘텐츠를 빨리 볼 수 있지만, 만약 웹사이트가 자바스크립트에 의존적이라면 사용자가 정상적인 페이지를 보기 전까지 서버에서 자바스크립트를 받아오는 시간과 실행하는 시간을 기다려야 하는 단점이 있다.
<br><br>

---

<br>

## head + async

```javascript
<html lang='ko'>
  <head>
    <meta charset='UTF-8' />
    <title>Document</title>
    <script async src='main.js'></script>
  </head>
  <body>
    <div></div>
  </body>
</html>
```

async를 사용할 경우, 브라우저가 HTML의 흐름을 읽다가 자바스크립트를 읽을 때 병렬로 자바스크립트를 다운받으면서 흐름을 읽어내려가다 다운로드가 완료 되었을 때, 흐름을 멈추고 자바스크립트 파일을 실행하게 된다. 실행 후 다시 흐름을 읽기 시작한다. 장점으로는 병렬로 흐름을 읽는것인데, HTML의 흐름을 읽기도 전에 자바스크립트가 실행되는 단점이 있다.
<br><br>

---

<br>

## head + defer

```javascript
<html lang='ko'>
  <head>
    <meta charset='UTF-8' />
    <title>Document</title>
    <script defer src='main.js'></script>
  </head>
  <body>
    <div></div>
  </body>
</html>
```

defer을 사용할 경우, 병렬적으로 자바스크립트를 다운로드 후 HTML의 흐름이 끝난 후에 다운로드 된 자바스크립트를 실행하게 된다.
<br><br>

---

<br>

## 주의사항

<br>

```javascript
<html lang='ko'>
  <head>
    <title>Document</title>
    <script async src='a.js'></script>
    <script async src='b.js'></script>
    <script async src='c.js'></script>
  </head>
</html>
```

async로 다수의 자바스크립트를 다운로드 받게 되면, 정의된 순서와 상관없이 다운로드가 먼저 된 자바스크립트 순으로 실행하게 된다. 그러므로 HTML이 자바스크립트의 순서에 의존적이라면 문제가 생길 수 있다.
<br><br>

### 반대로

<br>

```javascript
<html lang='ko'>
  <head>
    <title>Document</title>
    <script defer src='a.js'></script>
    <script defer src='b.js'></script>
    <script defer src='c.js'></script>
  </head>
</html>
```

defer은 HTML의 흐름을 읽는 동안 병렬적으로 자바스크립트를 모두 다운로드 해놓고 HTML의 흐름이 끝나면 자바스크립트를 순서대로 실행하기 때문에, 만약 자바스크립트 순서에 의존적이라면 defer이 적합하다.
<br><br>

### Tip

<br>

```javascript
'use strict';
```

**ECMAScript 5에 추가된 'use strict';**

자바스크립트는 유연한 언어이기 때문에 선언되지 않은 변수에 값을 할당하든, 기존에 존재하는 프로토타입을 변경해도 에러가 나지 않는다.<br>
그러므로 순수 바닐라 자바스크립트를 사용 시 상단 부분에 정의해주면 비상식적인 에러를 잡아주는 역할을 한다.
