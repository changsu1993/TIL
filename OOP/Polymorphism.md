# 1. 다형성 (Polymorphism)

하나의 변수가 서로 다른 클래스의 인스턴스를 가리킬 수 있는 성질을 다형성이라 한다. (여러 가지의 형태를 갖는 성질)

```python
from math import pi

class Rectangle:
    """직사각형 클래스"""
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        """직사각형의 넓이를 리턴한다"""
        return self.width * self.height

    def perimeter(self):
        """직사각형의 둘레를 리턴한다"""
        return 2 * self.width + 2 * self.height

    def __str__(self):
        """직사각형의 정보를 문자열로 리턴한다"""
        return "밑변 {}, 높이 {}인 직사각형".format(self.width, self.height)


class Circle:
    """원 클래스"""
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        """원의 넓이를 리턴한다"""
        return pi * self.radius * self.radius

    def perimeter(self):
        """원의 둘레를 리턴한다"""
        return 2 * pi * self.radius

    def __str__(self):
        """원의 정보를 문자열로 리턴한다"""
        return "반지름 {}인 원".format(self.radius)


class Cylinder:
    """원통 클래스"""
    def __init__(self, radius, height):
        self.radius = radius
        self.height = height

    def __str__(self):
    """원통의 정보를 문자열로 리턴하는 메소드"""
        return "밑면 반지름 {}, 높이 {}인 원기둥".format(self.radius, self.height)


class Paint:
    """그림판 프로그램 클래스"""
    def __init__(self):
        self.shapes = []

    def add_shape(self, shape):
        """그림판에 도형을 추가한다"""
        self.shapes.append(shape)

    def total_area_of_shapes(self):
        """그림판에 있는 모든 도형의 넓이의 합을 구한다"""
        return sum([shape.area() for shape in self.shapes])

    def total_perimeter_of_shapes(self):
        """그림판에 있는 모든 도형의 둘레의 합을 구한다"""
        return sum([shape.perimeter() for shape in self.shapes])

    def __str__(self):
        """그림판에 있는 각 도형들의 정보를 출력한다."""
        res_str = "그림판 안에 있는 도형들:\n\n"
        for shape in self.shapes:
            res_str += str(shape) + "\n"
        return res_str
```

shape이 Rectangle 인스턴스 또는 Circle 인스턴스를 가리키는 것을 다형성이라 볼 수 있다.

<br><br>

### 추상클래스 <br>

여러 클래스들의 공통점을 추상화해서 모아놓은 클래스

```python
from abc import ABC, abstractmethod
# 대문자 ABC는 Abstract Base Class 줄임말 (추상화 기초 클래스)

class Shape(ABC):
  """도형 클래스"""
  @abstractmethod
  def area(self):
    """도형의 넓이를 리턴한다: 자식 클래스가 오버라이딩할 것"""
    pass

  @abstractmethod
  def perimeter(self):
    """도형의 둘레를 리턴한다: 자식 클래스가 오버라이딩할 것"""
    pass

# Shape을 상속받는 클래스는 반드시 area 메소드와 perimeter 메소드를 오버라이딩 해야 한다.
```

어떤 클래스를 추상 클래스로 만들려면 abc라는 모듈에서 ABC라는 클래스와 abstractmethod 메소드라는 데코레이터 함수를 import 해야 한다. <br>
ABC 클래스를 상속받으면 추상 클래스로 만들 수 있다. <br>
추상 클래스를 만들기 위해서는 추상 메소드도 필요하다. 추상 메소드는 자식 클래스가 반드시 오버라이딩 해야 되는 메소드이다. <br>
어떤 메소드를 추상 메소드로 만들려면 import 해놓은 abstractmethod 데코레이터 함수를 사용하면 된다. <br>
추상 메소드가 최소한 1개 이상 있어야 추상 클래스라고 할 수 있다. <br>

정리해보자면 추상 클래스는 ABC 클래스를 상속받고 적어도 하나 이상의 추상 메소드를 가져야 한다. <br>
추상 클래스는 인스턴스를 직접 생성하려고 쓰는 클래스가 아닌 여러 클래스들의 공통점을 담아두고 다른 클래스들이 상속받는 부모 클래스가 될 목적으로 존재하기 때문에 추상 클래스로는 인스턴스를 만들 수 없다.
