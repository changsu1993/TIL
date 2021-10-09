# 1. preventDefault

## preventDefault

html에서 표준으로 제공하는 태그의 기본 이벤트 발생을 막는 메서드이다.

```javascript
const checkbox = document.querySelector('input');
checkbox.addEventListener('click', (event) => {
  console.log('checked');
  event.preventDefault();
});

// 콘솔에 checked는 출력되지만 체크박스에 체크는 되지 않는다.
```

반면,

```javascript
document.addEventListener('wheel', (event) => {
  console.log('scrolling');
  event.preventDefault();
});

// 이 때에는 preventDefault가 무시된다.
```

그 이유는 빠르게 뭔가가 동작해야 되는 이벤트는 브라우저가 무시하게 된다. 즉, passive(수동)하게 등록된다. <br>
이 때, 해결할 수 있는 방법으로는 addEventListener에 passive 옵션을 쓰면 해결할 수 있다. <br>
passive는 true, false로 사용할 수 있다. (passive: true => passive , passive: false => active) <br>

다만, 스크롤링 처럼 passive가 기본값이 true로 설정된 것들은 기본값을 건들지 않는 게 좋다.
<br><br>
