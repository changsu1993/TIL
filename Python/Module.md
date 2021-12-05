# 1. Module (모듈)

모듈(module)이란 함수나 변수 또는 클래스들을 모아 놓은 파일이다. <br>
다른 파이썬 프로그램에서 불러와 사용할 수 있게끔 만들어진 파이썬 파일이라고도 할 수 있다.

<br>

```python
# calculator.py

def add(x, y):
    return x + y


def subtract(x, y):
    return x - y


def multiply(x, y):
    return x * y


def divide(x, y):
    return x / y
```

```python
# run.py

import calculator # calculator 파이썬 파일 불러오기 (모듈)
import calculator as calc # as를 쓰면 모듈 이름을 변경할 수도 있다
from calculator import add, multiply # calculator 모듈에서 add 함수와 multiply 함수만 불러오겠다는 의미
from calculator import * # calculator 모듈에서 모든 함수를 불러오라는 의미
# *는 함수들의 출처가 불분명 해지기 때문에 권장하지 않는다.

calculator.add(1, 2) # 3
calc.add(1, 2) # 3
add(1, 2) # 3
multiply(1, 2) # 2
```

<br>

파이썬을 설치하면 표준 라이브러리(standard library)가 같이 딸려오는데 여기에는 다양한 모듈들이 있다. <br>
다양한 모듈들 중에서는 개발자들이 자주 쓸 법한 기능들도 상당 부분 만들어져 있다.

<br>

```python
import math # 표준 라이브러리 기본

math.log10(100) # 로그 함수
math.cos(0) # 코사인 함수
math.pi # 원주율 파이


import random # 표준 라이브러리 기본

random.random() # 0.0 ~ 1.0 사이의 랜덤한 수가 리턴
```
