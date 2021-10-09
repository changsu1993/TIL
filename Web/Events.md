# 1. Events

Event 인터페이스는 DOM 내에 위치한 이벤트를 나타낸다. 이벤트의 종류는 다양하며 일부는 Event 인터페이스의 파생 인터페이스를 사용하고 Event 자체는 모든 이벤트에 공통된 속성과 메서드를 가진다. <br>

**브라우저에서 발생할 수 있는 이벤트 참고** <br>
https://developer.mozilla.org/ko/docs/Web/Events

<br>

이벤트를 사용하기 위해선 특정한 요소에 Event Handler를 등록하면 된다. <br>
예를 들어, click 이벤트를 특정한 요소에 등록하고 click을 했을 때, 브라우저에서 이벤트라는 오브젝트를 만들어서 어떤 부분에서 클릭이 되었고 어떤 요소가 클릭이 되었는지 등 다양한 정보들이 들어있는 이벤트 오브젝트를 등록한 콜백 함수에 전달해주게 된다. <br>

모든 엘리먼트는 노드를 상속하고 노드는 이벤트 타겟을 상속하므로 모든 엘리먼트는 이벤트 타겟이라 볼 수 있다. 즉, 이벤트 핸들러를 다 등록할 수 있다. <br><br>

이벤트 타겟에는 총 3개의 API가 있다.

- EventTarget.addEventListener() **이벤트 리스너 추가**
- EventTarget.removeEventListener() **특정한 이벤트 리스너 제거**
- EventTarget.dispatchEvent() **인공적으로 이벤트 전달 및 발생**

<br><br>

## Event delegation

사용자의 액션에 의해 이벤트 발생 시 이벤트는 document 까지 버블링 되어 올라간다. 이 때문에 자식 엘리먼트에서 발생하는 이벤트를 부모 엘리먼트에서도 감지할 수 있다. 이러한 동작을 이용해 이벤트 위임을 할 수 있다. 특정 엘리먼트에 각각의 이벤트를 등록하지 않고 하나의 부모에 등록하여 부모에게 이벤트를 위임하는 방법이다.

```javascript
<ul>
  <li><button id="file">파일</button></li>
  <li><button id="edit">편집</button></li>
  <li><button id="view">보기</button></li>
</ul>

<script>
const ul = document.querySelector('ul');
ul.addEventListener('click', event => {
  if(target.id === 'file') {
    // 파일 메뉴 동작
  } else if (target.id === 'edit') {
    // 편집 메뉴 동작
  } else if (target.id === 'view') {
    // 보기 메뉴 동작
});
</script>
```
