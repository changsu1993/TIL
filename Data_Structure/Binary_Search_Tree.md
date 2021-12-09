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



def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)



class BinarySearchTree:
    """이진 탐색 트리 클래스"""
    def __init__(self):
        self.root = None

    def print_sorted_tree(self):
        """이진 탐색 트리 내의 데이터를 정렬된 순서로 출력해주는 메소드"""
        print_inorder(self.root)  # root 노드를 in-order로 출력한다.

# 비어 있는 이진 탐색 트리 생성
bst = BinarySearchTree()

# 노드 인스턴스 생성
node_0 = Node(5)
node_1 = Node(3)
node_2 = Node(7)

node_0.left_child = node_1
node_0.right_child = node_2

node_1.parent = node_0
node_2.parent = node_0
```

<br>

**이진 탐색 트리 삽입**

삽입 이후에도 이진 탐색 트리 속성이 유지되어야 한다. <br>
이진 탐색 트리에서는 트리의 높이를 이용해서 시간 복잡도를 분석한다. <br>
트리의 높이: h <br>

- 새로운 노드를 생성한다. O(1)
- root 노드부터 비교하면서 저장할 위치를 찾는다. 최악의 경우 O(h)
- 찾은 위치에 새롭게 만든 노드를 연결한다. O(1)

삽입 시간 복잡도는 O(h)이다.

<br>

**이진 탐색 트리 삽입 구현**

```python
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.right_child = None
        self.left_child = None


def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)


class BinarySearchTree:
    """이진 탐색 트리 클래스"""
    def __init__(self):
        self.root = None


    def insert(self, data):
        new_node = Node(data)  # 삽입할 데이터를 갖는 새 노드 생성

        # 트리가 비었으면 새로운 노드를 root 노드로 만든다
        if self.root is None:
            self.root = new_node
            return

        temp = self.root  # 저장하려는 위치를 찾기 위해 사용할 변수, root 노드로 초기화

        # 원하는 위치를 찾아간다
        while temp is not None:
            if data > temp.data:  # 삽입하려는 데이터가 현재 노드의 데이터보다 크다면
                # 오른쪽 자식이 없으면 새로운 노드를 현재 노드의 오른쪽 자식으로 만듦
                if temp.right_child is None:
                    new_node.parent = temp
                    temp.right_child = new_node
                    return
                # 오른쪽 자식이 있으면 오른쪽 자식으로 간다
                else:
                    temp = temp.right_child
            else:  # 삽입하려는 데이터가 현재 노드의 데이터보다 작다면
                if temp.left_child is None:
                    new_node.parent = temp
                    temp.left_child = new_node
                    return
                else:
                    temp = temp.left_child

    def print_sorted_tree(self):
        """이진 탐색 트리 내의 데이터를 정렬된 순서로 출력해주는 메소드"""
        print_inorder(self.root)  # root 노드를 in-order로 출력한다


# 빈 이진 탐색 트리 생성
bst = BinarySearchTree()

# 데이터 삽입
bst.insert(7)
bst.insert(11)
bst.insert(9)
bst.insert(17)
bst.insert(8)
bst.insert(5)
bst.insert(19)
bst.insert(3)
bst.insert(2)
bst.insert(4)
bst.insert(14)

# 이진 탐색 트리 출력
bst.print_sorted_tree()
```

<br>

**이진 탐색 트리 탐색**

특정 데이터를 갖는 노드를 리턴하는 연산이다. <br>
트리의 높이: h <br>

- 주어진 노드의 데이터와 탐색하려는 데이터 비교한다. (root 노드에서 시작)
- 탐색하려는 데이터가 더 크면 노드의 오른쪽 자식으로 간다.
- 탐색하려는 데이터가 더 작으면 노드의 왼쪽 자식으로 간다.
- 탐색하려는 노드를 찾으면 리턴한다.

탐색 시간 복잡도는 최악의 경우 O(h)이다.

 <br>

**이진 탐색 트리 탐색 구현**

```python
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.right_child = None
        self.left_child = None


def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)


class BinarySearchTree:
    """이진 탐색 트리 클래스"""
    def __init__(self):
        self.root = None


    def search(self, data):
        """이진 탐색 트리 탐색 메소드, 찾는 데이터를 갖는 노드가 없으면 None을 리턴한다"""
        temp = self.root  # 탐색용 변수, root 노드로 초기화

        # 원하는 데이터를 갖는 노드를 찾을 때까지 돈다
        while temp is not None:
            # 원하는 데이터를 갖는 노드를 찾으면 리턴
            if data == temp.data:
                return temp
            # 원하는 데이터가 노드의 데이터보다 크면 오른쪽 자식 노드로 간다
            elif data < temp.data:
                temp = temp.left_child
            # 원하는 데이터가 노드의 데이터보다 작으면 왼쪽 자식 노드로 간다
            elif data > temp.data:
                temp = temp.right_child

        return None  # 원하는 데이터가 트리에 없으면 None 리턴

    def insert(self, data):
        """이진 탐색 트리 삽입 메소드"""
        new_node = Node(data)  # 삽입할 데이터를 갖는 노드 생성

        # 트리가 비었으면 새로운 노드를 root 노드로 만든다
        if self.root is None:
            self.root = new_node
            return

        temp = self.root  # 저장하려는 위치를 찾기 위해 사용할 변수. root 노드로 초기화한다

        # 원하는 위치를 찾아간다
        while temp is not None:
            if data > temp.data:  # 삽입하려는 데이터가 현재 노드 데이터보다 크다면
                # 오른쪽 자식이 없으면 새로운 노드를 현재 노드 오른쪽 자식으로 만듦
                if temp.right_child is None:
                    new_node.parent = temp
                    temp.right_child = new_node
                    return
                # 오른쪽 자식이 있으면 오른쪽 자식으로 간다
                else:
                    temp = temp.right_child
            else:  # 삽입하려는 데이터가 현재 노드 데이터보다 작다면
                # 왼쪽 자식이 없으면 새로운 노드를 현재 노드 왼쪽 자식으로 만듦
                if temp.left_child is None:
                    new_node.parent = temp
                    temp.left_child = new_node
                    return
                # 왼쪽 자식이 있다면 왼쪽 자식으로 간다
                else:
                    temp = temp.left_child


    def print_sorted_tree(self):
        """이진 탐색 트리 내의 데이터를 정렬된 순서로 출력해주는 메소드"""
        print_inorder(self.root)  # root 노드를 in-order로 출력한다


# 빈 이진 탐색 트리 생성
bst = BinarySearchTree()

# 데이터 삽입
bst.insert(7)
bst.insert(11)
bst.insert(9)
bst.insert(17)
bst.insert(8)
bst.insert(5)
bst.insert(19)
bst.insert(3)
bst.insert(2)
bst.insert(4)
bst.insert(14)

# 노드 탐색과 출력
print(bst.search(7).data)
print(bst.search(19).data)
print(bst.search(2).data)
print(bst.search(20))
```

<br>

**이진 탐색 트리 삭제**

삭제하려는 데이터를 갖는 노드를 먼저 찾아야 된다.

- 경우 1: 삭제하려는 데이터가 leaf 노드의 데이터일 때

지우려는 노드가 부모 노드의 왼쪽 자식인지 오른쪽 자식인지 확인해서 각 경우에 맞게 None 처리를 해주면 된다.

- 경우 2: 삭제하려는 데이터 노드가 하나의 자식 노드만 있을 때

자식 노드가 부모 노드의 자리를 차지하면 된다.

- 경우 3: 삭제하려는 데이터의 노드가 두 개의 자식이 있을 때

<br>

```python
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.right_child = None
        self.left_child = None


def print_inorder(node):
    """주어진 노드를 in-order로 출력해주는 함수"""
    if node is not None:
        print_inorder(node.left_child)
        print(node.data)
        print_inorder(node.right_child)


class BinarySearchTree:
    """이진 탐색 트리 클래스"""
    def __init__(self):
        self.root = None


    def delete(self, data):
        """이진 탐색 트리 삭제 메소드"""
        node_to_delete = self.search(data)  # 삭제할 노드를 가지고 온다
        parent_node = node_to_delete.parent  # 삭제할 노드의 부모 노드

        # 경우 1: 지우려는 노드가 leaf 노드일 때
        if node_to_delete.left_child is None and node_to_delete.right_child is None:
            # 지우려는 노드가 root 노드일 때
            if self.root is node_to_delete:
                self.root = None
            else:
                if node_to_delete is parent_node.left_child:
                    parent_node.left_child = None
                else:
                    parent_node.right_child = None

        # 경우 2: 지우려는 노드가 자식이 하나인 노드일 때:
        # 지우려는 노드가 root 노드일 때
        elif node_to_delete.left_child is None:
            if node_to_delete is self.foot:
                self.root = node_to_delete.right_child
                self.root.parent = None

            # 지우려는 노드가 부모의 왼쪽 자식일 때
            elif node_to_delete is parent_node.left_child:
                parent_node.left_child = node_to_delete.right_child
                node_to_delete.right_child.parent = parent_node

            # 지우려는 노드가 부모의 오른쪽 자식일 때
            else:
                parent_node.right_child = node_to_delete.right_child
                node_to_delete.right_child.parent = parent_node

        # 지우려는 노드가 왼쪽 자식만 있을 때
        elif node_to_delete.right_child is None:
            # 지우려는 노드가 root 노드일 때
            if node_to_delete is self.root:
                self.root = node_to_delete.left_child
                self.root.parent = None

            # 지우려는 노드가 부모의 왼쪽 자식일 때
            elif node_to_delete is parent_node.left_child:
                parent_node.left_child = node_to_delete.left_child
                node_to_delete.left_child.parent = parent_node

            # 지우려는 노드가 부모의 오른쪽 자식일 때
            else:
                parent_node.right_child = node_to_delete.left_child
                node_to_delete.left_child.parent = parent_node

        # 경우 3: 지우려는 노드가 2개의 자식이 있을 때
        else:
            successor = self.find_min(node_to_delete.right_child) # 삭제하려는 노드의 successor 노드 받아오기
            node_to_delete.data = successor.data # 삭제하려는 노드의 데이터에 successor의 데이터 저장

            if successor is successor.parent.left_child: # successor 노드가 오른쪽 자식일 때
                successor.parent.left_child = successor.right_child
            else: # successor 노드가 왼쪽 자식일 때
                successor.parent.right_child = successor.right_child

            if successor.right_child is not None: # successor 노드가 오른쪽 자식이 있을 때
                successor.right_child.parent = successor.parent


    @staticmethod
    def find_min(node):
        """(부분)이진 탐색 트리의 가장 작은 노드 리턴"""
        temp = node  # 탐색용 변수, 파라미터 node로 초기화

        # temp가 node를 뿌리로 갖는 부분 트리에서 가장 작은 노드일 때까지 왼쪽 자식 노드로 간다
        while temp.left_child is not None:
            temp = temp.left_child

        return temp


    def search(self, data):
        """이진 탐색 트리 탐색 메소드, 찾는 데이터를 갖는 노드가 없으면 None을 리턴한다"""
        temp = self.root  # 탐색용 변수, root 노드로 초기화

        # 원하는 데이터를 갖는 노드를 찾을 때까지 돈다
        while temp is not None:
            # 원하는 데이터를 갖는 노드를 찾으면 리턴
            if data == temp.data:
                return temp
            # 원하는 데이터가 노드의 데이터보다 크면 오른쪽 자식 노드로 간다
            if data > temp.data:
                temp = temp.right_child
            # 원하는 데이터가 노드의 데이터보다 작으면 왼쪽 자식 노드로 간다
            else:
                temp = temp.left_child

        return None # 원하는 데이터가 트리에 없으면 None 리턴


    def insert(self, data):
        """이진 탐색 트리 삽입 메소드"""
        new_node = Node(data)  # 삽입할 데이터를 갖는 노드 생성

        # 트리가 비었으면 새로운 노드를 root 노드로 만든다
        if self.root is None:
            self.root = new_node
            return

        temp = self.root  # 저장하려는 위치를 찾기 위해 사용할 변수. root 노드로 초기화한다

        # 원하는 위치를 찾아간다
        while temp is not None:
            if data > temp.data:  # 삽입하려는 데이터가 현재 노드 데이터보다 크다면
                # 오른쪽 자식이 없으면 새로운 노드를 현재 노드 오른쪽 자식으로 만듦
                if temp.right_child is None:
                    new_node.parent = temp
                    temp.right_child = new_node
                    return
                # 오른쪽 자식이 있으면 오른쪽 자식으로 간다
                else:
                    temp = temp.right_child
            else:  # 삽입하려는 데이터가 현재 노드 데이터보다 작다면
                # 왼쪽 자식이 없으면 새로운 노드를 현재 노드 왼쪽 자식으로 만듦
                if temp.left_child is None:
                    new_node.parent = temp
                    temp.left_child = new_node
                    return
                # 왼쪽 자식이 있다면 왼쪽 자식으로 간다
                else:
                    temp = temp.left_child


    def print_sorted_tree(self):
        """이진 탐색 트리 내의 데이터를 정렬된 순서로 출력해주는 메소드"""
        print_inorder(self.root)  # root 노드를 in-order로 출력한다


# 빈 이진 탐색 트리 생성
bst = BinarySearchTree()

# 데이터 삽입
bst.insert(7)
bst.insert(11)
bst.insert(9)
bst.insert(17)
bst.insert(8)
bst.insert(5)
bst.insert(19)
bst.insert(3)
bst.insert(2)
bst.insert(4)
bst.insert(14)

# leaf 노드 삭제
bst.delete(2)
bst.delete(4)

bst.print_sorted_tree()
```

<br>

**이진 탐색 트리 삭제 연산 시간 복잡도**

탐색

이진 탐색 트리의 높이를 h라고 했을 때, 탐색 연산은 O(h)의 시간 복잡도가 걸린다. <br>

삭제 경우1: 지우려는 데이터 노드가 leaf 노드일 때

탐색한 노드의 부모에서 자식 레퍼런스를 None으로 지정해주면 된다. 걸리는 시간이 노드 개수나 트리 높이에 비례하지 않는다. O(1)
<br><br>

삭제 경우2: 지우려는 데이터 노드가 하나의 자식이 있을 때

삭제하려는 노드의 부모의 자식을 삭제하려는 노드의 자식으로 만들어 줬는데 이 때는 어떤 노드인지와 상관없이 레퍼런스 2개만 연결시켜 주면 된다. O(1)
<br><br>

삭제 경우3: 지우려는 데이터 노드가 두 개의 자식이 있을 때

1. 먼저 지우려는 데이터 노드의 successor 노드를 찾는다. O(h)
2. 지우려는 노드에 successor 노드의 데이터를 저장한 후 O(h)
3. successor 노드를 지운다. O(1)

합치면 총 O( h + h + 1)이 걸린다. 즉, O(h) 이다.
<br><br>

**정리**

삭제 연산 시 3가지 경우들의 시간 복잡도

|       | 탐색 | 탐색 후 단계들 |
| ----- | ---- | -------------- |
| 경우1 | O(h) | O(1)           |
| 경우2 | O(h) | O(1)           |
| 경우3 | O(h) | O(h)           |

<br><br>

탐색 후 단계들의 시간 복잡도에 제외해두었던 탐색 연산 자체의 시간 복잡도 O(h)까지 더해주면

|       | 탐색 + 탐색 후 단계들 |     |
| ----- | --------------------- | --- |
| 경우1 | O(h)                  |     |
| 경우2 | O(h)                  |     |
| 경우3 | O(h)                  |     |

<br><br>

**이진 탐색 트리 높이**

이진 탐색 트리 연산들의 시간은 모두 그 높이 h에 비례한다.

- 편향된 트리일수록 연산들이 비효율적으로,
- 균형이 잡힌 트리일수록 연산들이 효율적으로

이루어진다고 볼 수 있다.
<br><br>

**정리**

| 이진 탐색 트리 연산 | 시간 복잡도                       |     |
| ------------------- | --------------------------------- | --- |
| 삽입                | O(h) (평균적 O(lg(n)), 최악 O(n)) |     |
| 탐색                | O(h) (평균적 O(lg(n)), 최악 O(n)) |     |
| 연산                | O(h) (평균적 O(lg(n)), 최악 O(n)) |     |

<br><br>

**이진 탐색 트리로 딕셔너리 구현하기**

```python
class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, data):
        self.data = data
        self.parent = None
        self.left_child = None
        self.right_child = None


# 딕셔너리용 이진 탐색 트리 노드

class Node:
    """이진 탐색 트리 노드 클래스"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.parent = None
        self.left_child = None
        self.right_child = None
```

<br>

**시간 복잡도**

| 이진 탐색 트리 연산                   | 시간 복잡도                    |     |
| ------------------------------------- | ------------------------------ | --- |
| key를 이용한 key-value 데이터 쌍 삭제 | O(h) (평균 시간 복잡도 O(lg(n) |     |
| key를 이용한 노드 또는 value 탐색     | O(h) (평균 시간 복잡도 O(lg(n) |     |
| key-value 쌍 삽입                     | O(h) (평균 시간 복잡도 O(lg(n) |     |
