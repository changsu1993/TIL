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
random.randint(1, 20) # 두 수 사이의 랜덤한 정수를 리턴
random.uniform(0, 1) # 두 수 사이의 랜덤한 소수를 리턴


import os # operating system (운영 체제)
# os 모듈은 파이썬으로 우리의 운영 체제를 조작하기 위함

os.getlogin() # 현재 컴퓨터에 어떤 계정으로 로그인 되어있는지 알 수 있다
os.getcwd() # 현재 이 파일이 있는 폴더의 경로를 받아올 수 있다


import datetime # 날짜와 시간을 다루기 위한 다양한 클래스를 갖추고 있다.

# datetime 값 생성
pi_day = datetime.datetime(2020, 3, 14, 13, 6, 15)
print(pi_day) # 2020-03-14 13:06:15

# 오늘 날짜
today = datetime.datetime.now()
print(today)

# timedelta (날짜 간의 차이를 나타내는 타입)
today = datetime.datetime.now()
pi_day = datetime.datetime(2020, 3, 14, 13, 6, 15)
print(today - pi_day)
# 반대로 timedelta를 생성해서 datetime값에 더해줄 수도 있다.
today = datetime.datetime.now()
my_timedelta = datetime.timedelta(days=5, hours=3, minutes=10, seconds=50)
print(today + my_timedelta)

# datetime 해부
today = datetime.datetime.now()

print(today)
print(today.year)  # 연도
print(today.month)  # 월
print(today.day)  # 일
print(today.hour)  # 시
print(today.minute)  # 분
print(today.second)  # 초
print(today.microsecond)  # 마이크로초

# datetime 포맷팅
# strftime을 사용하면 입맛대로 바꿀 수 있다.
today = datetime.datetime.now()

print(today)
print(today.strftime("%A, %B %dth %Y"))

포맷 코드	설명	예시
%a	요일 (짧은 버전)	Mon
%A	요일 (풀 버전)	Monday
%w	요일 (숫자 버전, 0~6, 0이 일요일)	5
%d	일 (01~31)	23
%b	월 (짧은 버전)	Nov
%B	월 (풀 버전)	November
%m	월 (숫자 버전, 01~12)	10
%y	연도 (짧은 버전)	16
%Y	연도 (풀 버전)	2016
%H	시간 (00~23)	14
%I	시간 (00~12)	10
%p	AM/PM	AM
%M	분 (00~59)	34
%S	초 (00~59)	12
%f	마이크로초 (000000~999999)	413215
%Z	표준시간대	PST
%j	1년 중 며칠째인지 (001~366)	162
%U	1년 중 몇 주째인지 (00~53, 일요일이 한 주의 시작이라고 가정)	35
%W	1년 중 몇 주째인지 (00~53, 월요일이 한 주의 시작이라고 가정)	35
```
