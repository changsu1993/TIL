# 1. LBYL & EAFP

### LBYL (Look Before You Leap) <br>

어떤 작업을 수행하기 전에 그 작업을 수행해도 괜찮을지 확인하는 것

```python
class Paint:
    """그림판 프로그램 클래스"""
    def __init__(self):
        self.shapes = []

    def add_shape(self, shape):
        """그림판에 도형을 추가한다"""
        if isinstance(shape, Shape):
            self.shapes.append(shape)
        else:
            pirnt("도형 클래스가 아닌 인스턴스는 추가할 수 없습니다.")

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

<br>

### EAFP (Easier to Ask Forgiveness than Permission) <br>

어떤 상황이든 일단 먼저 빨리 실행하고 문제가 생기면 그 때 처리하자는 식의 사고방식

```python
class Paint:
    """그림판 프로그램 클래스"""
    def __init__(self):
        self.shapes = []

    def add_shape(self, shape: Shape):
        """그림판에 도형 인스턴스 shape을 추가한다. 단, shape은 추상 클래스 Shape의 인스턴스여야 한다."""
        self.shapes.append(shape)


    def total_area_of_shapes(self):
        """그림판에 있는 모든 도형의 넓이의 합을 구한다"""
        total_area = 0

        for shape in self. shapes:
          try:
              total_area += shape.area()
          except (AttributeError, TypeError):
              print("그림판에 area 메소드가 없거나 잘못 정의되어 있는 인스턴스 {}가 있습니다.".format(shape))

        return total_area

    def total_perimeter_of_shapes(self):
        """그림판에 있는 모든 도형의 둘레의 합을 구한다"""
        total_perimeter = 0

        for shape in self.shapes:
            try:
                total_perimeter += shape.perimeter()
            except (AttributeError, TypeError):
                print("그림판에 perimeter 메소드가 없거나 잘못 정의되어 있는 인스턴스 {}가 있습니다.".format(shape))

        return total_perimeter

    def __str__(self):
        """그림판에 있는 각 도형들의 정보를 출력한다."""
        res_str = "그림판 안에 있는 도형들:\n\n"
        for shape in self.shapes:
            res_str += str(shape) + "\n"
        return res_str
```

<br>
