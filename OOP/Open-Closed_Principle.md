# 1. 개방 폐쇄 원칙 (Open-Closed Principle)

클래스는 확장에 열려 있어야 하며, 수정에는 닫혀 있어야 한다. <br>
확장에 열려 있다는 건 프로그램의 기존 기능을 확장할 수 있다는 것이고 수정에 닫혀 있다는 건 한 번 작성한 코드를 바꾸지 않아도 되는 것이다. <br>
즉, 어떤 클래스의 코드를 수정하지 않아도 기존 기능을 확장할 수 있어야 한다.

```python
class AppleKeyboard:
    """애플 키보드 클래스"""

    def __init__(self):
        """키보드 인풋과 터치바 인풋"""
        self.keyboard_input = ""

    def set_keyboard_input(self, input):
        """키보드 인풋 설정 메소드"""
        self.keyboard_input = input

    def send_keyboard_input(self):
        """키보드 인풋 전송 메소드"""
        return self.keyboard_input

class SamsungKeyboard:
    """삼성 키보드 클래스"""

    def __init__(self):
        """키보드 인풋과 터치바 인풋"""
        self.user_input = ""

    def save_user_input(self, input):
        """키보드 인풋 설정 메소드"""
        self.user_input = input

    def give_user_input(self):
        """키보드 인풋 전송 메소드"""
        return self.user_input


class KeyboardManager:
    def __init__(self):
        """키보드 관리 클래스"""
        self.keyboard = None

    def connect_to_keyboard(self, keyboard):
        """키보드 교체 메소드"""
        self.keyboard = keyboard

# 새로운 키보드를 입력할 때마다 메소드를 변경해줘야 하는 상황이 발생.
# 개방폐쇄원칙을 준수하지 못함.
    def get_keyboard_input(self):
        """유저가 키보드로 입력한 내용을 받아오는 메소드"""
        if isinstance(self.keyboard, AppleKeyboard):
          return self.keyboard.send_keyboard_input()
        else isinstance(SELF.KEYBOARD, SansungKeyboard):
          return self.keyboard.give_user_input()

keyboard_manager = KeyboardManager()

apple_keyboard = AppleKeyboard()

keyboard_manager.connect_to_keyboard(apple_keyboard)

apple_keyboard.set_keyboard_input("안녕하세요")

print(keyboard_manager.get_keyboard_input())

# ====================================================
# 다형성을 사용하여 개방폐쇄원칙 지키기 (추상클래스)

from abc import ABC, abstractmethod

class Keyboard(ABC):
    """키보드 클래스"""
    @abstractmethod
    def save_input(self, content: str) -> None:
        """키보드 인풋 저장 메소드"""
        pass

    @abstractmethod
    def send_input(self) -> str:
        """키보드 인풋 전송 메소드"""
        pass

class AppleKeyboard(Keyboard):
    """애플 키보드 클래스"""
    def __init__(self):
        """키보드 인풋과 터치바 인풋"""
        self.keyboard_input = ""

    def save_input(self, input):
        """키보드 인풋 설정 메소드"""
        self.keyboard_input = input

    def send_input(self):
        """키보드 인풋 전송 메소드"""
        return self.keyboard_input

class SamsungKeyboard(Keyboard):
    """삼성 키보드 클래스"""

    def __init__(self):
        """키보드 인풋과 터치바 인풋"""
        self.user_input = ""

    def save_input(self, input):
        """키보드 인풋 설정 메소드"""
        self.user_input = input

    def send_input(self):
        """키보드 인풋 전송 메소드"""
        return self.user_input

class KeyboardManager:
    def __init__(self):
        """키보드 관리 클래스"""
        self.keyboard = None

    def connect_to_keyboard(self, keyboard):
        """키보드 교체 메소드"""
        self.keyboard = keyboard

    def get_keyboard_input(self):
        """유저가 키보드로 입력한 내용을 받아오는 메소드"""
        return self.keyboard.send_input()
```

<br>

**_개방폐쇄원칙을 지키는 이유_** <br>
더 쉽게 협력하고 더 편하게 수정하기 위해서!
