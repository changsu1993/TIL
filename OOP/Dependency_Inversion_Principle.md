# 1. 의존 관계 역전 원칙 (Dependency Inversion Principle)

의존 관계 역전 원칙의 정의는 상위 모듈은 하위 모듈의 구현 내용에 의존하면 안 되고 상위 모듈과 하위 모듈 모두 추상화된 내용에 의존해야 한다는 것이다. <br>
두 클래스가 있을 때 어떤 클래스가 다른 클래스를 사용하는 관계에 있으면 <br>
이때 사용하는 클래스를 상위 모듈, 사용 당하는 클래스를 하위 모듈이라 생각하면 된다.

```python
# 상위 모듈인 GameCharacter 클래스가, 하위 모듈인 Sword 클래스의 구현 내용에 의존하고 있다.

class Sword:
    """검 클래스"""
    def __init__(self, damage):
        self.damage = damage

    def slash(self, other_character):
        """검 사용 메소드"""
        other_character.get_damage(self.damage)


class GameCharacter:
    """게임 캐릭터 클래스"""
    def __init__(self, name, hp, sword: Sword):
        self.name = name
        self.hp = hp
        self.sword = sword

    def attack(self, other_character):
        """다른 유저를 공격하는 메소드"""
        if self.hp > 0:
            self.sword.slash(other_character)
        else:
            print(self.name + "님은 사망해서 공격할 수 없습니다.")

    def change_sword(self, new_sword):
        """검을 바꾸는 메소드"""
        self.sword = new_sword

    def get_damage(self, damage):
        """캐릭터가 공격받았을 때 자신의 체력을 깎는 메소드"""
        if self.hp <= damage:
            self.hp = 0
            print(self.name + "님은 사망했습니다.")
        else:
            self.hp -= damage

    def __str__(self):
        """남은 체력을 문자열로 리턴하는 메소드"""
        return self.name + "님은 hp: {}이(가) 남았습니다.".format(self.hp)
```

<br><br>

```python
from abc import ABC, abstractmethod

class IWeapon(ABC):
    """무기 클래스"""
    @abstractmethod
    def use_on(self, other_character):
        pass

class Sword(IWeapon):
    """검 클래스"""
    def __init__(self, damage):
        self.damage = damage

    def use_on(self, other_character):
        """검 사용 메소드"""
        other_character.get_damage(self.damage)

class Gun(IWeapon):
    """총 클래스"""
    def __init__(self, damage, num_rounds):
        self.damage = damage
        self.num_rounds = num_rounds  # 총알 갯수

    def use_on(self, other_character):
        if self.num_rounds > 0:
            other_character.get_damage(self.damage)
            self.num_rounds -= 1
        else:
            print("총알이 없어 공격할 수 없습니다")

class GameCharacter:
    """게임 캐릭터 클래스"""
    def __init__(self, name, hp, weapone: IWeapon):
        self.name = name
        self.hp = hp
        self.weapone = weapone

    def attack(self, other_character):
        """다른 유저를 공격하는 메소드"""
        if self.hp > 0:
            self.weapone.use_on(other_character)
        else:
            print(self.name + "님은 사망해서 공격할 수 없습니다.")

    def change_sword(self, new_sword):
        """검을 바꾸는 메소드"""
        self.sword = new_sword

    def get_damage(self, damage):
        """캐릭터가 공격받았을 때 자신의 체력을 깎는 메소드"""
        if self.hp <= damage:
            self.hp = 0
            print(self.name + "님은 사망했습니다.")
        else:
            self.hp -= damage

    def __str__(self):
        """남은 체력을 문자열로 리턴하는 메소드"""
        return self.name + "님은 hp: {}이(가) 남았습니다.".format(self.hp)
```

<br>

이처럼 추상 클래스로 상위 모듈과 하위 모듈 사이에 추상화 레이어를 만들면 해결할 수 있다. <br>

1. 상위 모듈에는 추상 클래스의 자식 클래스의 인스턴스를 사용한다는 가정 하에 그 하위 모듈을 사용하는 코드를 작성해두면 되고,
2. 하위 모듈은 추상 클래스의 추상 메소드들을 구현(오버라이딩)만 하면 된다. <br>

의존 관계 역전 원칙은 개방-패쇄 원칙을 지키는 하나의 방법이다.
