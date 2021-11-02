# 1. 리스코프 치환 원칙 (Liskov Substitution Principle)

부모 클래스의 인스턴스를 사용하는 위치에 자식 클래스의 인스턴스를 대신 사용했을 때 코드가 원래 의도대로 작동해야 한다는 의미이다. <br>

자식 클래스의 인스턴스는 부모 클래스의 인스턴스이기도 하다.<br>
이런 성질 때문에 부모 클래스의 인스턴스가 들어갈 자리에 자식 클래스의 인스턴스를 넣을 수도 있다. <br>
리스코프 치환 원칙은 이때 자식 클래스의 인스턴스가 부모 클래스의 인스턴스가 행동하는 범위 내에서 행동해야 한다는 원칙이다. <br>
즉, 부모 클래스의 행동규약을 자식 클래스가 위반하지 말라는 것이다. <br>

부모 클래스의 행동규약을 자식 클래스가 어긴다는 것은 자식 클래스가 오버라이딩을 잘못 하는 경우를 말한다. <br>

1. 자식 클래스가 부모 클래스의 변수의 타입을 바꾸거나 메소드의 파라미터 또는 리턴값의 타입 또는 갯수를 바꾸는 경우
2. 자식 클래스가 부모 클래스의 의도와 다르게 메소드를 오버라이딩 하는 경우

<br><br>

```python
class Employee:
    """직원 클래스"""
    company_name = "코드잇 버거"
    raise_percentage = 1.03

    def __init__(self, name, wage):
        self.name = name
        self._wage = wage

    def raise_pay(self):
        """직원 시급을 인상하는 메소드"""
        self._wage *= self.raise_percentage

    @property
    def wage(self):
        return self._wage

    def __str__(self):
        """직원 정보를 문자열로 리턴하는 메소드"""
        return Employee.company_name + " 직원: " + self.name


class Cashier(Employee):
    """리스코프 치환 원칙을 지키지 않는 계산대 직원 클래스"""
    burger_price = 4000

    def __init__(self, name, wage, number_sold=0):
        super().__init__(name, wage)
        self.number_sold = number_sold

# 오버라이딩 후 멋대로 raise_amount 파라미터 추가 (규칙 위반)
    def raise_pay(self, raise_amount):
        """직원 시급을 인상하는 메소드"""
        self.wage += self.raise_amount

# 리턴값을 str로 멋대로 수정 (규칙 위반)
    @property
    def wage(self):
        return "시급 정보를 알려줄 수 없습니다"
```

<br><br>

**리스코프 치환 원칙에 따라 수정**

```python
class Employee:
    """직원 클래스"""
    company_name = "코드잇 버거"
    raise_percentage = 1.03

    def __init__(self, name, wage):
        """인스턴스 변수 설정"""
        self.name = name
        self._wage = wage

    def raise_pay(self):
        """직원 시급을 인상하는 메소드"""
        self._wage *= self.raise_percentage

    @property
    def wage(self):
        """_wage 변수 getter 메소드"""
        return self._wage

    def __str__(self):
        """직원 정보를 문자열로 리턴하는 메소드"""
        return Employee.company_name + " 직원: " + self.name


class Cashier(Employee):
    """계산대 직원 클래스"""
    raise_percentage = 1.05
    burger_price = 4000

    def __init__(self, name, wage, number_sold=0):
        super().__init__(name, wage)
        self.number_sold = number_sold

    def take_order(self, money_received):
        """손님이 낸 돈을 받아 주문 처리를 하고 거스름돈을 리턴한다"""
        if Cashier.burger_price > money_received:
            print("돈이 충분하지 않습니다. 돈을 다시 계산해서 주세요!")
            return money_received
        else:
            self.number_sold += 1
            change = money_received - Cashier.burger_price
            return change

    def __str__(self):
        return Cashier.company_name + " 계산대 직원: " + self.name
```
