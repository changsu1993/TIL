# 1. 단일 책임 원칙 (Single Responsibility Principle)

모든 클래스는 단 한가지의 책임만을 갖고, 클래스 안에 정의되어 있는 모든 기능은, 이 하나의 책임을 수행하는데 집중되어 있어야 한다. <br>
즉, 하나의 클래스로 너무 많은 일을 하지 말고 딱 한 가지 책임만 수행하라는 뜻이다. <br><br>

GOD Object(하나의 클래스가 많은 책임을 직접 수행하는 객체) 예시

```python
class Ship:
    """배 클래스"""
    def __init__(self, fuel, fuel_per_hour, supplies, num_crew):
        """연료량, 시간당 연료 소비량, 물자량, 선원 수를 인스턴스 변수로 갖는다"""
        self.fuel = fuel
        self.fuel_per_hour = fuel_per_hour
        self.supplies = supplies
        self.num_crew = num_crew

    def report_fuel(self):
        """연료량 보고 메소드"""
        print("현재 연료는 {}l 남아 있습니다".format(self.fuel))

    def load_fuel(self, amount):
        """연료 충전 메소드"""
        self.fuel += amount

    def report_supplies(self):
        """물자량 보고 메소드"""
        print("현재 물자는 {}명분이 남아 있습니다".format(self.supplies))

    def load_supplies(self, amount):
        """물자 보급 메소드"""
        self.supplies += amount

    def distribute_supplies_to_crew(self):
        """물자 배분 메소드"""
        if self.supplies >= self.num_crew:
            self.supplies -= self.num_crew
            return True
        print("물자가 부족하기 때문에 배분할 수 없습니다")
        return False

    def report_crew(self):
        """선원 수 보고 메소드"""
        print("현재 선원 {}명이 있습니다".format(self.num_crew))

    def load_crew(self, number):
        """선원 승선 메소드"""
        self.num_crew += number

    def run_engine_for_hours(self, hours):
        """엔진 작동 메소드"""
        if self.fuel > self.fuel_per_hour * hours:
            self.fuel -= self.fuel_per_hour * hours
            print("엔진을 {}시간 동안 돌립니다!".format(hours))
        else:
            print("연료가 부족하기 때문에 엔진 작동을 시작할 수 없습니다")
```

<br><br>
단일책임원칙 적용

```python
class Ship:
    """배 클래스"""
    def __init__(self, fuel, fuel_per_hour, supplies, num_crew):
        self.fuel_tank = FuelTank(fuel)
        self.crew_manager = CrewManager(num_crew)
        self.supply_hold = SupplyHold(supplies, self.crew_manager)
        self.engine = Engine(self.fuel_tank, fuel_per_hour)


class FuelTank:
    """연료 탱크 클래스"""
    def __init__(self, fuel):
        """연료 탱크에 저장된 연료량을 인스턴스 변수로 갖는다"""
        self.fuel = fuel

    def load_fuel(self, amount):
        """연료 충전 메소드"""
        self.fuel += amount

    def use_fuel(self, amount):
        """연료 사용 메소드"""
        if self.fuel - amount >= 0:
            self.fuel -= amount
            return True
        print("연료가 부족합니다!")
        return False

    def report_fuel(self):
        """연료량 보고 메소드"""
        print("현재 연료는 {}l 남아 있습니다".format(self.fuel))


class Engine:
    """엔진 클래스"""
    def __init__(self, fuel_tank, fuel_per_hour):
        """연료 탱크 인스턴스와 시간당 연료 소비량을 인스턴스 변수로 갖는다"""
        self.fuel_tank = fuel_tank
        self.fuel_per_hour = fuel_per_hour

    def run_for_hours(self, hours):
        """엔진 작동 메소드, 연료 탱크 인스턴스를 사용한다"""
        if self.fuel_tank.use_fuel(self.fuel_per_hour * hours):
            print("엔진을 {}시간 동안 돌립니다!".format(hours))
            return True
        print("연료가 부족하기 때문에 엔진 작동을 시작할 수 없습니다")
        return False


class CrewManager:
    """선원 관리 클래스"""
    def __init__(self, num_crew):
        """승선한 선원 수를 인스턴스 변수로 갖는다"""
        self.num_crew = num_crew

    def load_crew(self, number):
        """선원 승선 메소드"""
        self.num_crew += number

    def report_crew(self):
        """선원 수 보고 메소드"""
        print("현재 선원 {}명이 있습니다".format(self.num_crew))


class SupplyHold:
    """물자 창고 클래스"""
    def __init__(self, supplies, crew_manager):
        """물자량과 선원 관리 인스턴스를 인스턴스 변수로 갖는다"""
        self.supplies = supplies
        self.crew_manager = crew_manager

    def load_supplies(self, amount):
        """물자 충전 메소드"""
        self.supplies += amount

    def distribute_supplies_to_crew(self):
        """물자 배분 메소드, 각 선원들에게 동일한 양의 물자를 배분한다"""
        if self.supplies >= self.crew_manager.num_crew:
            self.supplies -= self.crew_manager.num_crew
            return True
        print("물자가 부족하기 때문에 배분할 수 없습니다")
        return False

    def report_supplies(self):
        """물자량 보고 메소드"""
        print("현재 물자는 {}명분이 남아 있습니다".format(self.supplies))
```

<br>
