# 1. Decorator

파이썬은 데코레이터 기능을 제공한다. <br>
데코레이터란 함수를 받아 명령을 추가한 뒤 이를 다시 함수의 형태로 반환하는 함수이다. <br>
일반적으로 함수의 전처리나 후처리에 대한 필요가 있을 때 사용하고 함수의 내부를 수정하지 않고 기능에 변화를 주고 싶을 때 사용한다. <br>
또한 데코레이터를 이용해 반복을 줄이고 메소드나 함수의 책임을 확장한다.

```python
# 데코레이터 함수
def add_print_to(original):
  def wrapper():
    print('함수시작')
    original
    print('함수 끝')
  return wrapper

@add_print_to # print_hello 함수를 add_print_to로 꾸며주라는 뜻
def print_hello():
print('안녕하세요')

print_hello()
```

```python
def add_print_to(original):
  def wrapper():
    print('함수시작')
    original
    print('함수 끝')
  return wrapper

@add_print_to
def function1():
  기존 함수1 내용

@add_print_to
def function2():
  기존 함수2 내용

@add_print_to
def function3():
  기존 함수3 내용
```
