# 1. Linked List

링크드 리스트는 노드라는 단위의 데이터를 저장하고 데이터가 저장된 각 노드들을 순서대로 연결시켜서 만든 자료구조이다. <br>
동적 배열처럼 계속해서 새로운 요소를 추가할 수 있다. <br>
각 노드는 하나의 객체로 표현된다. 노드 객체 안에는 data 속성과 next 속성 두 가지가 존재한다. <br>
data 속성에는 저장하고 싶은 정보를 넣고 next 속성에는 다음 노드에 대한 래퍼런스를 넣는다. <br>
노드 객체들은 메모리에 연속적으로 저장된 게 아닌 메모리 여기 저기에 흩어져 저장되어 있지만 각 노드는 next 속성에 다음 노드에 대한 래퍼런스가 있기 때문에 정보를 원하는 순서로 저장할 수 있다. <br> 링크드 리스트의 시작점 역할을 하는 첫 번째 노드 객체를 head 노드라 한다.
<br><br>

**노드 클래스 만들기**

```python
class Node:
    """링크드 리스트의 노드 클래스"""

    def __init__(self, data):
        self.data = data  # 노드가 저장하는 데이터
        self.next = None  # 다음 노드에 대한 레퍼런스


# 데이터 2, 3, 5, 7, 11을 담는 노드들 생성
head_node = Node(2)
node_1 = Node(3)
node_2 = Node(5)
node_3 = Node(7)
tail_node = Node(11)

# 노드들을 연결
head_node.next = node_1
node_1.next = node_2
node_2.next = node_3
node_3.next = tail_node

# 노드 순서대로 출력
iterator = head_node

while iterator is not None:
    print(iterator.data)
    iterator = iterator.next
```

<br>

```python
# 간단한 링크드 리스트 만들기

class Node:
    """링크드 리스트의 노드 클래스"""

    def __init__(self, data):
        self.data = data  # 노드가 저장하는 데이터
        self.next = None  # 다음 노드에 대한 레퍼런스

class LinkedList:
    """링크드 리스트 클래스"""

    def __init__(self):
        self.head = None
        self.tail = None

    def pop_left(self):
        """링크드 리스트의 가장 앞 노드 삭제 메소드. 단, 링크드 리스트에 항상 노드가 있다고 가정한다"""
        data = self.head.data

        if self.head is self.tail:
            self.head = None
            self.tail = None
        else:
            self.head = self.head.next

        return data

    def delete_after(self, previous_node):
        """링크드 리스트 삭제연산. 주어진 노드 뒤 노드를 삭제한다"""
        data = previous_node.next.data

        # 지우려는 노드가 tail 노드일 때:
        if previous_node.next is self.tail:
            previous_node.next = None
            self.tail = previous_node
        # 두 노드 사이 노드를 지울 때:
        else:
            previous_node.next = previous_node.next.next

        return data

    def insert_after(self, previous_node, data):
        """링크드 리스트 주어진 노드 뒤 삽입 연산 메소드"""
        new_node = Node(data)

        # 가장 마지막 순서 삽입
        if previous_node is self.tail:
            self.tail.next = new_node
            self.tail = new_node
        else:  # 두 노드 사이에 삽입
            new_node.next = previous_node.next
            previous_node.next = new_node


    def find_node_at(self, index):
        """링크드 리스트 접근 연산 메소드. 파라미터 인덱스는 항상 있다고 가정"""
        iterator = self.head

        for _ in range(index):
            iterator = iterator.next

        return iterator

    def append(self, data):
        """링크드 리스트 추가 연산 메소드"""
        new_Node = Node(data)

        if self.head is None:  # 링크드 리스트가 비어 있는 경우
            self.head = new_node
            self.tail = new_node
        else:  # 링크드 리스트가 비어 있지 않은 경우
            self.tail.next = new_node
            self.tail = new_node


# 링크드 리스트 접근 시간 복잡도

# 인덱스를 이용해서 링크드 리스트 노드에 접근하는 건 치명적인 단점이 있다.
# 접근하고 싶은 인덱스가 x라고 하면 헤드 노드에서 총 x번 다음 노드로 가야 한다.
# 배열은 인덱스에 상관없이 항상 일정하게 한 번에 접근할 수 있었던 반면
# 링크드 리스트는 더 뒤에 있는 노드에 접근할수록 점점 더 드는 시간이 늘어난다.
# 마지막 노드에 접근하려면 head에서 다음 노드로 n-1 번 가야 한다.
# 실행되는데 걸리는 시간이 n에 비례하기 때문에 접근 연산의 시간 복잡도는 최악의 경우 O(n)이다.
```

<br><br>

## 링크드 리스트 연산들 시간 복잡도

### 접근

인덱스 x에 있는 데이터에 접근하려면 링크드 리스트의 head 노드부터 x번 다음 노드를 찾아서 가야 한다. <br>
즉, 원하는 노드에 접근하는 시간은 몇 번째 인덱스인지에 비례한다. <br>
링크드 리스트 안에 있는 노드의 수를 n이라고 하면, 마지막 순서에 있는 노드에 접근해야 되는 최악의 경우에는 head 노드에서 총 n-1번 다음 노드로 가야 된다. 걸리는 시간은 n에 비례하기 때문에 접근 연산은 최악의 경우 O(n)의 시간 복잡도를 갖는다.
<br><br>

### 탐색

링크드 리스트 탐색 연산은 배열을 탐색할 때와 같은 방법으로 한다. <br>
가장 앞 노드부터 다음 노드를 하나씩 보면서 원하는 데이터를 찾는다. <br>
접근과 마찬가지로 링크드 리스트 안에 찾는 데이터가 없을 때 또는 찾으려는 데이터가 마지막 노드에 있는 최악의 경우, n개의 노드를 모두 다 봐야한다. 그렇기 때문에 탐색도 접근과 마찬가지로 최악의 경우 O(n)의 시간 복잡도를 갖는다.
<br><br>

### 삽입/삭제

삽입, 삭제는 그냥 삽입, 삭제할 인덱스의 주변 노드들에 연결된 레퍼런스만 수정한다. <br>
즉, 실행되는데 걸리는 시간은 특정 값에 비례하지 않고 항상 일정하다. <br>
파라미터로 받는 이 노드가 어떤 순서에 있든 노드든 상관없이 걸리는 시간은 변하지 않는다. <br>
O(1)의 시간 복잡도를 갖는다 할 수 있다. <br>

가장 앞에 접근 + 삽입 = O(1+1) <br>
가장 앞에 접근 + 삭제 = O(1+1) <br>
가장 뒤에 접근 + 삽입 = O(1+1) <br>
원하는 노드에 접근 또는 탐색 + 삽입 or 삭제 = O(n+1)
<br><br>
