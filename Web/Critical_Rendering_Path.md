# 1. Critical Rendering Path

브라우저가 서버에서 페이지에 대한 HTML 응답을 받으면 화면에 표시하기까지 많은 단계를 거친다. 브라우저가 페이지의 출력을 위해 실행해야 하는 순서를 랜더링 경로(Critical Rendering Path, CRP)라 한다.

CRP는 6단계로 구성된다.

- DOM 트리 구축 (Constructing the DOM Tree)
- CSSOM 트리 구축 (Constructing the CSSOM Tree)
- JavaScript 실행 (Running JavaScript)
- 랜더링 트리 구축 (Creating the Render Tree)
- layout 생성 (Generating the Layout)
- paint (Painting)

<br>

**DOM 트리 구축** <br>
루트 요소 \<html>로 시작해 페이지의 각 element/text에 대한 노드가 만들어진다. 다른 요소 내에 중첩된 요소는 자식 노드로 표시되며 각 노드에 해당 요소의 전체 특성이 포함된다. <br><br>
**CSSOM 트리 구축** <br>
HTML을 파싱하다 CSS 링크를 만나면, CSS파일을 요청해 받아오게 된다. 받아온 CSS파일은 HTML을 파싱한 것과 유사한 과정을 거쳐 Tree형태의 CSSOM으로 만들어진다. CSS 파싱은 자식 노드가 부모 노드의 특성을 이어받는 cascading 규칙이 추가되는 것 말고는 HTML 파싱과 동일하게 이어진다. <br><br>
**JavaScript 실행** <br>
HTML 문서 자체의 구문 분석은 JavaScript에 의해 차단된다. (parser blocking resource) <br>
\<script> 태그에 도달하면 fetch를 중단하고 실행하기 때문에, 문서 안에 요소를 참조하는 JavaScript 파일이 있는 경우 해당 문서가 표시된 후에 배치해야 한다. <br>
JavaScript가 parser blocking 되는 것을 피하기 위한 방법으로는 async 또는 defer 속성을 적용하여 비동기적으로 로드할 수 있다. <br><br>
**랜더링 트리 구축** <br>
DOM과 CSSOM을 합쳐 Render Tree를 만든다. 페이지에 최종적으로 랜더링 될 내용을 나타내는 트리이다. 화면에 실제로 표시되는 내용만으로 이루어지기 때문에 display: none, \<head> 태그 등은 추가되지 않는다. <br><br>
**레이아웃 생성** <br>
Render Tree에 있는 각각의 노드들이 어디에 위치할 지 계산하는 layout 과정을 거치게 된다. 레이아웃은 뷰포트의 크기에 관련된 CSS 스타일에 대한 컨텍스트에 의해 뷰포트의 크기를 결정한다. CSS box model이 쓰이며 position, width, height 등 틀과 위치에 관련된 부분들이 계산된다. 만약 width: 70%인 브라우저를 리사이즈 한다면, 보이는 요소들은 변함이 없기 때문에 Render Tree는 그대로인 상태에서, layout 단계만 다시 거쳐 위치를 계산해서 그리게 된다. <br><br>
**페인트** <br>
Render Tree의 각 노드들을 실제로 화면에 그리게 된다. 페이지의 가시적인 내용을 픽셀로 변환하여 화면에 표시할 수 있다. 페인팅 단계에서 처리에 걸리는 시간은 DOM의 크기와 적용되는 스타일에 따라 달라진다. 복잡한 그라디언트 배경 이미지는 단순한 단색보다 더 많은 시간을 필요로 한다. <br>
만약 Render Layer 2개 이상이라면 각각의 Layer를 paint한 뒤 하나의 이미지로 Composite하는 과정을 추가로 거친 뒤 실제 화면에 그려지게 된다.
<br><br>

6단계를 2개의 카테고리로 나눌 수 있다. <br>

- Construction <br>
  HTML 페이지에서 브라우저가 이해할 수 있도록 브라우저만의 언어로 바꾸는 파트 <br>
  (DOM 요소가 작으면 작을수록, CSS규칙이 작으면 작을수록 Tree가 작아지기 때문에 빠르게 만들 수 있다.) <br>
  (DOM -> CSSOM -> Render Tree) <br><br>
- Operation <br>
  만들어진 랜더링 트리를 이용해서 구조를 작성하고 어디에 배치할 것인지 계산 후 실제 브라우저 윈도우에 랜더링 하는 파트 <br>
  (사용자에게 표기하는 것도 중요하지만 사용자가 클릭으로 요소를 움직이거나 애니메이션을 쓸 때 페인트가 자주 일어나지 않게 만드는 것이 중요하다.) <br>
  (layout -> paint -> composition)
