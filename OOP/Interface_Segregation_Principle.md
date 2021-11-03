# 1. 인터페이스 분리 원칙 (Interface Segregation Principle)

인터페이스란 추상 클래스 중에서 추상 메소드만 있고 일반 메소드는 없는 것을 말한다. <br>
인터페이스 분리 원칙의 정의는 클래스가 사용하지 않을 메소드에 의존할 것을 강요하면 안된다는 것이다. <br>
즉, 클래스가 나중에 사용하지도 않을 메소드를 가지도록 강제하지 말라는 뜻이다.
<br><br>

```python
from abc import ABC, abstractmethod

class IMessage(ABC):
    @property
    @abstractmethod
    def content(self):
        """추상 getter 메소드"""
        pass

    @abstractmethod
    def edit_content(self, new_content: str) -> None:
        """작성한 메시지를 수정하는 메소드"""
        pass

    @abstractmethod
    def send(self, destination: str) -> bool:
        """작성한 메시지를 전송하는 메소드"""
        pass


class Email(IMessage):
    def __init__(self, content, owner_email):
        """이메일은 그 내용과 보낸 사람의 이메일 주소를 인스턴스 변수로 가짐"""
        self._content = content
        self.owner_email = owner_email

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        """이메일 내용 수정 메소드"""
        self._content = self.owner_email + "님의 메일\n" + new_content

    def send(self, destination):
        """이메일 전송 메소드"""
        print("{}에서 {}로 이메일 전송!\n내용: {}").format(self.owner_email, destination, self._content)
        return True


class TextMessage(IMessage):
    def __init__(self, content):
        """문자 메시지는 그 내용을 인스턴스 변수로 가짐"""
        self._content = content

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        """문자 메시지 내용 수정 메소드"""
        self._content = new_content

    def send(self, destination):
        """문자 메시지 전송 메소드"""
        print("{}로 문자 메시지 전송!\n내용: {}").format(destination, self._content)


class TextReader:
    """인스턴스의 텍스트 내용을 읽어주는 클래스"""

    def __init__(self):
        self.texts = []

    def add_text(self, text: IMessage):
        """인스턴스 추가 메소드, 파라미터는 IMessage 인터페이스를 상속받을 것"""
        self.texts.append(text)

    def read_all_texts(self):
        """인스턴스 안에 있는 모든 텍스트 내용 출력"""
        for text in self.texts:
            print(text.content)

class Memo(Imessage):
    def __init__(self, content):
        """메모는 그 내용을 인스턴스 변수로 가짐"""
        self._content = content

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        self._content = new_content

    def send(self, destination):
        """메모는 전송할 수 없음"""
        print("메모는 아무 데도 보낼 수 없습니다.")
        return False
```

<br>

인터페이스 분리 원칙을 위반하지 않는 방법으로는 인터페이스를 더 작은 인터페이스로 나누는 방법이다. <br>
나눠진 작은 인터페이스는 역할 인터페이스(role interface)라 한다.
<br><br>

```python
from abc import ABC, abstractmethod

class IText(ABC):
    @property
    @abstractmethod
    def content(self):
        """추상 getter 메소드"""
        pass

    @abstractmethod
    def edit_content(self, new_content: str) -> None:
        """작성한 메시지를 수정하는 메소드"""
        pass

class ISendable(ABC):
    @abstractmethod
    def send(self, destination: str) -> bool:
        """작성한 메시지를 전송하는 메소드"""
        pass

class Email(IText, ISendable):
    def __init__(self, content, owner_email):
        """이메일은 그 내용과 보낸 사람의 이메일 주소를 인스턴스 변수로 가짐"""
        self._content = content
        self.owner_email = owner_email

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        """이메일 내용 수정 메소드"""
        self._content = self.owner_email + "님의 메일\n" + new_content

    def send(self, destination):
        """이메일 전송 메소드"""
        print("{}에서 {}로 이메일 전송!\n내용: {}").format(self.owner_email, destination, self._content)
        return True


class TextMessage(IText, ISendable):
    def __init__(self, content):
        """문자 메시지는 그 내용을 인스턴스 변수로 가짐"""
        self._content = content

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        """문자 메시지 내용 수정 메소드"""
        self._content = new_content

    def send(self, destination):
        """문자 메시지 전송 메소드"""
        print("{}로 문자 메시지 전송!\n내용: {}").format(destination, self._content)

class Memo(IText):
    def __init__(self, content):
        """메모는 그 내용을 인스턴스 변수로 가짐"""
        self._content = content

    @property
    def content(self):
        """_content 변수 getter 메소드"""
        return self._content

    def edit_content(self, new_content):
        self._content = new_content

class TextReader:
    """인스턴스의 텍스트 내용을 읽어주는 클래스"""

    def __init__(self):
        self.texts = []

    def add_text(self, text: IText):
        """인스턴스 추가 메소드, 파라미터는 IMessage 인터페이스를 상속받을 것"""
        self.texts.append(text)

    def read_all_texts(self):
        """인스턴스 안에 있는 모든 텍스트 내용 출력"""
        for text in self.texts:
            print(text.content)
```

<br>

인터페이스 분리 원칙을 정리해보자면 <br>

이 원칙은 지나치게 많은 추상 메소드를 가진 거대한 인터페이스 하나를, 관련된 추상 메소드들만 모여있도록 작은 크기의 인터페이스로 분리하라는 뜻이다. 이렇게 해야 하는 이유는 지나치게 큰 인터페이스는 그걸 상속하는 클래스가 자신에게 필요하지도 않은 메소드를 굳이 오버라이딩 하도록 만들기 때문이다. <br>

인터페이스가 서로 관련성이 높은, 적절한 개수의 추상 메소드들을 포함하게 될 때 그걸 역할 인터페이스(role interface)라고 한다. 큰 인터페이스 하나가 있는 것보다는 작은 역할 인터페이스 여러 개가 있으면 각 클래스가 본인에 해당하는 인터페이스만 적절히 상속받게 된다. 그럼 각 클래스가 어떤 기능을 갖는지 더 세밀하게 파악할 수 있게 해준다는 장점도 있다. <br>
