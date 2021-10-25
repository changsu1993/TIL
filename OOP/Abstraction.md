# 1. 추상화(Abstraction)

프로그래밍에서 추상화란 프로그래머들이 특정 코드를 사용할 때 필수적인 정보를 제외한 세부사항을 가리는 것을 말한다. <br>
쉽게 말해 어떤 사물에서 사용에 꼭 필요한 부분만 겉으로 드러내서 사용자가 겉으로 드러난 부분만 알면 되는 것을 추상화라 할 수 있다. <br><br>

### 추상화 잘하기 <br>

**이름 잘 짓기** <br>
(클래스, 변수, 메소드 등)이름을 잘 지어야 어디에 쓰는 것인지 파악하기 쉽다. <br><br>

**문서화 하기(docstring)** <br>
(documentation string) <br>

```python
"""
docstring
여러 줄을 써도 하나의 docstring 이다.
"""
```

docstring은 설명하고 싶은 클래스나 메소드 이름 바로 아래에 써준다. <br>
문서에 설명되어있는 docstring을 깔끔하게 한눈에 보고 싶다면 help(클래스 이름 또는 메소드 이름) 함수를 쓰면 된다. <br><br>
**문서화 스타일** <br>
널리 쓰이는 포맷 3가지 <br>

```python
def find_suggestion_videos(self, number_of_suggestions=5):

# Google docstring:
"""유저에게 추천할 영상을 찾아준다
Parameters:
  number_of_suggestions (int): 추천하고 싶은 영상 수
    (기본값은 5)

Returns:
  list: 추천할 영상 주소가 담긴 리스트
"""

# reStructuredText(파이썬 공식 문서화 기준):
"""유저에게 추천할 영상을 찾아준다

:param number_of_suggestions: 추천하고 싶은 영상 수
  (기본값은 5)
:type number_of_suggestions: int
:returns: 추천할 영상 주소가 담긴 리스트
:rtype: list
"""

# NumPy/SciPy (통계, 과학 분야에서 쓰이는 Python 라이브러리):
"""유저에게 추천할 영상을 찾아준다

Parameters
----------
number_of_suggestions: int
  추천하고 싶은 영상 수 (기본값은 5)

Returns
-------
list
  추천할 영상 주소가 담긴 리스트
"""
```

<br>

### type hinting <br>

정적타입 언어처럼 타입을 표시할 수 있는 기능 <br>

```python
test: float = 0.01

def find_suggestion_videos(self, number_of_suggestions: int) -> None:
```

type hinting은 파악하기 쉽게 해주는 역할이고 실행에 직접 영향을 주지 않는다. <br> python 3.5 이전 버전에서는 작동하지 않는다.
