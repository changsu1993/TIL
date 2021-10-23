# 1. Class & Instance

**클래스(Class)** 란 객체를 만들어 내기 위한 틀 혹은 설계도이다. (연관되어 있는 변수와 메서드의 집합) <br>

**객체(Object)** 란 소프트웨어 세계에 구현할 대상이다. 클래스에 선언된 모양 그대로 생성된 실체이다. 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖고 클래스의 인스턴스(instance)라고도 부른다. OOP의 관점에서 클래스의 타입으로 선언되었을 때 객체라고 부른다. <br>

**인스턴스(Instance)** 란 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체이다. 즉, 객체를 소프트웨어에 실체화 하면 그것을 인스턴스라고 부른다. 실체화된 인스턴스는 메모리에 할당된다. 인스턴스는 객체에 포함된다고 볼 수 있다. OOP의 관점에서 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다. 추상적인 개념과 구체적인 객체 사이의 관계에 초점을 맞출 경우에 사용한다.
<br><br>

## Method(메소드)

객체 안에 속성은 인스턴스 변수로 나타내고 행동은 함수로 나타낸다. (객체의 행동을 나타내는 함수를 메소드라 한다.) 즉, 클래스 안에 함수를 정의하면 메소드를 정의했다고 볼 수 있다.
<br><br>

### 메소드의 종류

1. 인스턴스 메소드
2. 클래스 메소드
3. 정적 메소드

<br>

### 인스턴스 메소드 <br>

인스턴스 변수를 사용하거나, 인스턴스 변수에 값을 설정하는 메소드

```python
class User:
  def say_hello(some_user):
    print("안녕하세요. 저는 {}입니다.".format(some_user.name))

user1 = User()

user1.name = "파이썬"
user1.email = "python@gamil.com"
user1.password = "1234"

User.say_hello(user1)
# 클래스 이름.메소드 이름(인스턴스) 또는
user1.say_hello()
# 인스턴스 이름.메소드 이름()

# 인스턴스 메소드의 특별한 규칙
# 인스턴스에 메소드를 호출하면 인스턴스가 첫 번째 파라미터로 자동으로 전달된다.
# 파이썬에서 인스턴스 메소드를 사용할 때 첫 번째 파라미터는 self로 쓰도록 권장하고 있다.
class User:
  def say_hello(self):
    print("안녕하세요. 저는 {}입니다.".format(self.name))

user1 = User()

user1.name = "파이썬"
user1.email = "python@gamil.com"
user1.password = "1234"

user1.say_hello()
```

<br>

### 특수 메소드 (magic method or special method) <br>

특정 상황에서 자동으로 호출되는 메소드(인스턴스가 생성될 때 자동으로 호출) <br>
이름 앞 뒤로 언더바가 두 개씩 존재

```python
class User:
  def __init__(self, name, email, password):
    self.name = name
    self.email = email
    self.password = password

user1 = User("Python", "python@gamil.com", "1234")
# 1. User 인스턴스 생성
# 2. __init__메소드 자동 호출
# self에는 생성된 User인스턴스가 들어간다.
# 그 후 괄호 안에 값들이 순서대로 들어간다.
# 인스턴스 변수들의 초기값 설정
```

```python
class User:
  def __init__(self, name, email, password):
    self.name = name
    self.email = email
    self.password = password

# double underscore (dunder 메소드)
  def __str__(self):
    return "사용자: {}, 이메일: {}, 비밀번호: ******".format(self.name, self.email)
# print 함수를 호출할 때 자동으로 불리는 역할

user1 = User("Python", "python@gamil.com", "1234")
print(user1)
```

<br>

### 클래스 메소드 <br>

클래스 변수의 값을 읽거나 설정하는 메소드 <br>

```python
class User:
  count = 0

  def __init__(self, name, email, password):
    self.name = name
    self.email = email
    self.password = password

    User.count += 1

# double underscore (dunder 메소드)
  def __str__(self):
    return "사용자: {}, 이메일: {}, 비밀번호: ******".format(self.name, self.email)
# print 함수를 호출할 때 자동으로 불리는 역할

  @classmethod
  def number_of_users(cls):
    print("사용자 수{}".format(cls.count))
# cls는 User 클래스를 나타낸다
```

**클래스 메소드의 규칙** <br>

클래스 메소드는 메소드 위에 @classmethod(데코레이터)를 쓴다. <br>
첫 번째 파라미터로 cls를 쓴다. (python의 약속)
<br><br>

**인스턴스 메소드와 클래스 메소드의 차이** <br>

```python
# 인스턴스 메소드
User.say_hello(user1)
user1.say_hello() # 인스턴스 자신이 첫 번째 파라미터로 자동 전달

# 클래스 메소드
User.number_of_users()
user1.number_of_users()
# 두 가지 방법 모두 첫 번째 파라미터로 클래스 자동 전달
# 클래스가 자동 전달 되는 이유는 @classmethod 데코레이터로 number_of_users를 클래스 메소드로 만들어줬기 때문이다.
```

<br>

**클래스 변수와 인스턴스 변수 둘 다 쓸 경우** <br>

인스턴스 메소드는 인스턴스 변수와 클래스 변수 모두 사용 가능하다. (인스턴스 변수는 self를 통해, 클래스 변수는 클래스 이름에 .을 붙여서) <br>
반면 클래스 메소드는 인스턴스 변수를 사용할 수 없다.
