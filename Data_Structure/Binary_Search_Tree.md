# 1. Binary Search Tree (이진 탐색 트리)

이진 탐색 트리는 딕셔너리나 세트 등의 추상 자료형을 구현하는 데 쓸 수 있다. <br>
이진 탐색 트리는 이진 트리지만 완전 이진 트리라는 보장은 없다. <br>
그렇기 때문에 보통 배열이나 파이썬 리스트를 써서 구현하지 않고 노드 클래스를 정의한 후 여러 노드 인스턴스들을 생성하고 이 인스턴스들을 연결시켜서 구현한다.

<br>

**이진 탐색 트리의 속성**

특정 노드를 봤을 때 왼쪽 부분 트리에 있는 모든 노드는 그 노드의 데이터보다 작아야 한다. <br>
그리고 오른쪽 부분에 있는 모든 노드는 그 노드의 데이터보다 커야 한다.

<br>

**이진 탐색 트리 노드 구현**

```python
class Node:
    """이진 트리 노드"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.left_child = None
        self.right_child = None

# 노드 인스턴스 생성
node_0 = Node(5)
node_1 = Node(3)
node_2 = Node(7)
```
