# 1. Object

파이썬은 순수 객체 지향 언어이다. 즉, 파이썬의 모든 것이 객체이다. <br>

```python
print(type(5)) # class int
print(type("string")) # class str
print(type([])) # class list
print(type({})) # class dict
print(type(())) # class tuple
```

<br>

객체에는 가변 타입 객체와 불변 타입 객체 두 가지 타입으로 나눌 수 있다. <br>
어떤 타입이냐에 따라서 같은 상황에서도 다른 결과를 나타낸다.<br>

가변 타입 객체 : 한번 생성한 인스턴스의 속성 변경 가능 (list, dict, 직접 작성하는 클래스)<br>
불변 타입 객체 : 한번 생성한 인스턴스의 속성 변경 불가 (bool, int, float, str, tuple) <br>
<br>

```python
mutable_object = [1, 2, 3]
immutable_object = (1, 2, 3)

mutable_object[0] = 5
print(mutable_object) # [5,2,3]

immutable_object[0] = 5
print(immutable_object) # TypeError
```

<br>
불변 타입 객체의 속성을 바꿀 수 없다고 해서 변수가 가리키는 객체 자체를 바꿀 수 없는 것은 아니다.
<br><br>

```python
tuple_x = (1,2)
tuple_x = (3,4)
tuple_x = (5,6,7)

print(tuple_x) # (5,6,7)
```
