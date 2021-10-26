# 1. 상속 (Inheritance)

상속이란 두 클래스 사이에 부모-자식 관계를 설정하는 것을 말한다.<br>
자식 클래스는 부모 클래스에 모든 변수와 메소드를 물려받는다. <br>
상속을 이용하려면 공통으로만 이루어진 부모 클래스를 만들어야 한다.

```python
class Employee:
  """직원 클래스"""
  company_name = "파이썬 버거" # 가게 이름
  raise_percentage = 1.03 # 시급 인상률

  def __init__(self, name, wage):
    self.name = name # 이름
    self.wage = wage # 시급

  def raise_pay(self):
    """시급을 인상하는 메소드"""
    self.wage *= self.raise_percentage

  def __str__(self):
    """직원 정보를 문자열로 리턴하는 메소드"""
    return Employee.company_name + " 직원: " + self.name

class Cashier(Employee):
  pass

class DeliveryMan(Employee):
  pass
```

<br>

### 상속과 관련된 메소드와 함수들 <br>

help 함수를 실행할 경우 Method resolution order: 라는 부분에 해당 인스턴스의 클래스가 어떤 부모 클래스를 가지는지 보여준다. 이 결과를 다른 방법으로도 볼 수 있다. <br>

**mro 메소드** <br>

```python
print(cashier.mro())

# 실행 결과
[<class '__main__.Cashier'>, <class '__main__.Employee'>, <class 'object'>]

print(list.mro())

# 실행 결과
[<class 'list'>, <class 'object'>]
```

<br>

**isinstance 함수** <br>

isinstance 함수는 어떤 인스턴스가 주어진 클래스의 인스턴스인지를 알려준다. <br>
isinstance 함수의 첫 번째 파라미터에는 검사할 인스턴스의 이름, 두 번째 파라미터에는 기준 클래스의 이름을 넣고 실행하면 된다. <br>
결과값으로 인스턴스가 해당 클래스의 인스턴스인지 불린 값으로 리턴한다. <br>

```python
# 인스턴스를 생성한다
young = Cashier("철수", 8900)

print(isinstance(young, Cashier)) # 출력: True
print(isinstance(young, DeliveryMan)) # 출력: False
print(isinstance(young, Employee)) # 출력: True

# 상속 관계에 있는 두 클래스가 있을 때, 자식 클래스로 만든 인스턴스는 부모 클래스의 인스턴스이기도 하다는 점
```

<br>

**issubclass 함수** <br>

issubclass 함수는 한 클래스가 다른 클래스의 자식 클래스인지를 알려주는 함수이다.<br>
첫 번째 파라미터로 검사할 클래스의 이름을 넣고 두 번째 파라미터에는 기준이 되는 부모 클래스의 이름을 넣으면 된다. <br>

```python
print(issubclass(Cashier, Employee)) # 출력: True
print(issubclass(Cashier, object)) # 출력: True
print(issubclass(Manager, Employee)) # 출력: True
print(issubclass(Employee, list)) # 출력: False
```

<br>

### 오버라이딩 (Overriding) <br>

부모 클래스로부터 물려받은 내용을 자식 클래스가 자신에 맞게 변경하는 걸 오버라이딩이라 한다. <br>
즉, 부모로부터 물려받은 걸 자기에 맞게 덮어써서 수정한다는 뜻이다. <br>

```python
class Employee:
  """직원 클래스"""
  company_name = "파이썬 버거" # 가게 이름
  raise_percentage = 1.03 # 시급 인상률

  def __init__(self, name, wage):
    self.name = name # 이름
    self.wage = wage # 시급

  def raise_pay(self):
    """시급을 인상하는 메소드"""
    self.wage *= self.raise_percentage

  def __str__(self):
    """직원 정보를 문자열로 리턴하는 메소드"""
    return Employee.company_name + " 직원: " + self.name

# 오버라이딩
class Cashier(Employee):
  raise_percentage = 1.05
  def __init__(self, name, wage, number_sold):
    super().__init__(name, wage)
    self.number_sold = number_sold

  def __str__(self):
    return Cashier.company_name + " 계산대 직원: " + self.name

class DeliveryMan(Employee):
  pass
```

super 함수는 자식 클래스에서 부모 클래스의 메소드를 사용하고 싶을 때 쓰는 함수이다. <br>
super 함수로 부모 클래스의 메소드를 사용할 때는 self 파라미터를 넘겨 줄 필요가 없다. (파이썬의 규칙) <br>
변수를 오버라이딩 하려면 그냥 자식 클래스에도 똑같은 이름의 변수를 두고 다른 값을 넣으면 된다.
