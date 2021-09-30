# 1. CSS 소개

Cascading Style Sheet,
HTML이나 XML로 작성된 문서의 표시 방법을 기술하기 위한 스타일 시트 언어이다.

웹사이트를 스타일링 할 때, 크게 3가지로 나눌 수 있다.

- Author Style
- User Style
- Browser

Author Style은 개발자가 웹사이트를 만들 때, 제공하는 CSS 파일이라 할 수 있다.

User Style은 브라우저 상에서 다크모드를 사용 또는 글자크기 조정 등 사용자의 취향에 맞게 브라우저에서 스타일링을 바꾸는 것이라 보면 된다.

Browser은 브라우저 상에서 기본적으로 지정된 스타일을 말한다.

3가지의 우선순위는 Author Style > User Style > Browser 이다.

CSS 스타일링을 정의할 때 **!important**를 쓸 경우 위 3가지의 우선순위를 무시하고 1순위가 되기 때문에 주의해야한다.
<br><br>

## Selectors(선택자)

Selectors는 HTML에 어떤 태그를 선택할 것인지에 대해 규정하는 문법이다.

- \*(Universal)
- Tag(type)
- #id(ID)
- .class(Class)
- :(State)
- \[](Attribute)
  <br><br>

```html
selector { property: value; }
```

<br>
Selectors(선택자)의 우선순위는<br>
!important(속성값) > style=""(인라인 스타일) > ID 선택자(#selector) > CLASS 선택자(.selector) == 속성 기반 선택자(a[href=""]) == 가상 클래스(a:hover) == 가상 요소(span::after) > 태그선택자(a) > 전체선택자(\*) 이다. <br><br>

### CSS 우선순위 규칙

- 원천 소스중 사용자 스타일시트가 가장 우선한다.
- 선택자 우선순위를 계산하여 값이 높은 순서대로 적용한다.
- 가장 마지막에 지정된 스타일을 우선적으로 적용한다.
  <br><br>

우선순위 계산은 가장 큰 값을 100을 기준으로<br>
선택자중 ID의 수를 세어 100,<br>
선택자중 가상 클래스와 클래스의 수를 세어 10,<br>
선택자중 엘리먼트의 수를 세어 1의 자리에 놓고 합산한다.<br>
가상 엘리먼트는 무시한다.
