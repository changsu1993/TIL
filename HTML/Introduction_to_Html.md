# 1. HTML 소개

HyperText Markup Language,
웹을 이루는 가장 기초적인 구성 요소로, 웹 콘텐츠의 의미와 구조를 정의할 때 사용한다.

HTML은 브라우저에서 실행 가능한 가장 기본적인 파일이고, 마크업 언어로 구조적으로 태그들을 이용해서 보여지며, \<html> 상위 태그 안에는 \<head> 와 \<body> 파트가 있다.

\<head> 안에는 상세설명이 들어가고, \<body> 안에는 사용자에게 보여지는 태그들로 이루어져 있다.

\<body> 안에 태그들은 BOX가 되는 태그들과 ITEM(사용자에게 보여지는 태그)이 되는 태그들로 분류된다.

BOX에는 header, section, footer, article, nav, div, aside, span, main, form 등이 있고 <br>
ITEM에는 a, video, button, audio, input, map, label, canvas, img, table 등이 있다.

사용자에게 보여지는 태그에는 Block Level Element 와 Inline Level Element로 나눌 수 있다.

Block Level Element는 태그를 사용해 요소를 삽입했을 때, 한 줄 전체를 차지하는 요소이다.

Inline Level Element는 줄을 차지하지 않는 요소이므로 한 줄에 여러 개의 인라인 레벨 요소를 표시하는 것이 가능하다.<br><br><br>

### **구조(명칭)**

```html
<p class="Attribute">Tag & Element & Attributes</p>
```

\<p> => Opening tag <br>
\</p> => Closing tag <br>
\<p>내용\</p> => 내용(Content) <br>
\<p>내용\</p> => 태그 전체포함 Element <br>
\<p> 태그 옆 class 부분이 Attribute 이다.
