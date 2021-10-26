# 1. 캡슐화 (Encapsulation)

캡슐화는 두 가지로 정의할 수 있다. <br>

1. 객체의 일부 구현 내용에 대한 외부로부터의 직접적인 액세스를 차단하는 것
2. 객체의 속성과 그것을 사용하는 행동을 하나로 묶는 것
   <br><br>

```python
# 첫 번째 정의 적용시키기
# 객체의 일부 구현 내용에 대한 외부로부터의 직접적인 액세스를 차단하는 것

class Citizen:
  """주민 클래스"""
  drinking_age = 19

  def __init__(self, name, age, resident_id):
    """이름, 나이, 주민등록번호"""
    self.name = name
    self.__age = age
    self.__resident_id = resident_id

  def authenticate(self, id_field):
    """본인이 맞는지 확인하는 메소드"""
    return self.__resident_id == id_field

  def can_drink(self):
    return self.__age >= Citizen.drinking_age

  def __str__(self):
    """주민 정보를 문자열로 리턴하는 메소드"""
    return self.name + "씨는" + str(self.__age) + "살입니다"

kyusik = Citizen("규식", 20, "12345678")
print(kyusik.__resident_id) # AttributeError __resident_id
print(kyusik.__age) # AttributeError __age
```

<br>
변수나 메소드 앞에 언더바 두 개를 붙이면 클래스 밖에서 접근이 불가능해진다.
<br><br>

```python
# 두 번째 정의 적용시키기
# 객체의 속성과 그것을 사용하는 행동을 하나로 묶는 것

class Citizen:
  """주민 클래스"""
  drinking_age = 19

  def __init__(self, name, age, resident_id):
    """이름, 나이, 주민등록번호"""
    self.name = name
    self.__age = age
    self.__resident_id = resident_id

  def authenticate(self, id_field):
    """본인이 맞는지 확인하는 메소드"""
    return self.__resident_id == id_field

  def can_drink(self):
    return self.__age >= Citizen.drinking_age

  def __str__(self):
    """주민 정보를 문자열로 리턴하는 메소드"""
    return self.name + "씨는" + str(self.__age) + "살입니다"

# 접근할 수 있는 메소드를 만드는 것
# 변수의 값을 읽는 메소드 getter 메소드
  def get_age(self):
    return self.__age

# 변수의 값을 설정하는 메소드 setter 메소드
  def set_age(self, value):
    return self.__age == value

# 주의사항
# 민감한 정보에 대해서는 값을 읽거나 설정하면 안 된다.
```

<br>

### 캡슐화 정리 <br>

1. 클래스 밖에서 접근 못하게 할 변수, 메소드 정하기
2. 변수나 메소드 이름 앞에 언더바 2개 붙이기
3. 변수에 간접 접근할 수 있게 메소드 추가하기(getter / setter or 다른 용도의 메소드)
   <br>

**주의** <br>

파이썬에서는 네임 맹글링(name mangling)이 있다. 네임 맹글링이란 변수나 메소드 이름 앞에 \_\_를 쓰면 파이썬은 그 앞에 추가적으로 '\_클래스 이름'을 덧붙여서 새로운 형태로 변환하는 것이다.<br>
변환된 이름으로 클래스 밖에서 접근할 수 있다. 사실 파이썬은 언어 차원에서 완벽한 캡슐화를 지원하지 않는다.
<br><br>

### 캡슐화와 파이썬 문화 <br>

변수나 메소드에 함부로 접근하지 말라는 의미에서 이름 앞에 언더바 하나를 써주면 된다. 언더바 하나는 변수나 메소드를 클래스 밖에서 직접 접근해서 사용하지 말라는 경고 표시다.
<br><br>

### 데코레이터를 사용한 캡슐화 <br>

```python
#_age의 getter 메소드 역할
@property
def age(self):
  print("나이를 리턴합니다.")
  return self._age

#_age의 setter 메소드 역할
@age.setter
def age(self, value):
  print("나이를 설정합니다.")
  if value < 0:
    print("나이는 0보다 작을 수 없습니다. 기본 값 0으로 나이를 설정하겠습니다.")
    self._age = 0
  else:
    self._age = value
```

property 데코레이터가 있으면 변수의 값을 읽거나 설정하는 구문이 아예 다른 의미로 실행된다. <br>
property 데코레이터를 사용하면 캡슐화 전 사용하던 코드를 캡슐화 후에 수정하지 않아도 된다.
