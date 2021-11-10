# 1. HashTable

하나의 key와 그 key에 해당하는 value를 합쳐서 key - value 쌍이다. <br>
하나의 key에는 하나의 value만 있어야 된다.

### Direct Access Table <br>

배열 인덱스를 키로 이용해서 데이터를 저장하고 가지고 오는 방식 <br>
효율적으로 key - value 쌍을 저장하고 가져올 수 있다. O(1) <br>
낭비하는 공간이 많다.

### 해시 함수 <br>

특정 값을 원하는 범위의 자연수로 바꿔주는 함수이다. <br>
해시 함수를 이용하면 키가 아무리 커도 항상 원하는 범위 사이의 자연수로 바꿀 수 있다. <br>

**해시 함수의 조건** <br>

1. 한 해시 테이블의 해시 함수는 결정론적이어야 된다.
2. 결과 해시값이 치우치지 않고 고르게 나온다.
3. 빨리 계산할 수 있어야 된다.

**해시 함수를 간단하게 만드는 두 가지 방법** <br>

나누기 방법 <br>
자연수 key를 해시 테이블의 크기로 나눈 나머지를 리턴하는 함수이다. <br>

```python
def hash_function_remainder(key, array_size):
    """해시 테이블의 key를 나누기 방법으로 0 ~ array_size - 1 범위의 자연수로 바꿔주는 함수"""
    return key % array_size


print(hash_function_remainder(40, 200))
print(hash_function_remainder(120, 200))
print(hash_function_remainder(788, 200))
print(hash_function_remainder(2307, 200))
```

<br>
곱셈 방법 <br>
예시로 key가 200, 사용하려는 배열 크기가 30이라면, <br>
먼저 0 < a < 1 인 아무 값 a를 정한다. <br>
그 다음에 a에 key를 곱한다. <br>
마지막으로 남은 소수 부분에 배열의 크기를 곱해준다.
<br><br>

```python
def hash_function_multiplication(key, array_size, a):
    """해시 테이블의 key를 곱셈 방법으로 0 ~ array_size - 1 범위의 자연수로 바꿔주는 함수"""
    temp = a * key # a와 key를 곱한다
    temp = temp - int(temp) # a와 key를 곱한 값의 소숫점 오른쪽 부분만 저장한다

    return int(array_size * temp) # temp와 배열 크기를 곱한 수의 자연수 부분만 리턴한다


print(hash_function_multiplication(40, 200, 0.61426212))
print(hash_function_multiplication(120, 200, 0.61426212))
print(hash_function_multiplication(788, 200, 0.61426212))
print(hash_function_multiplication(2307, 200, 0.61426212))
```

a와 key를 곱한 값의 정수 부분을 버리면 그 결과 값은 0.xxxx 이런 식으로 0과 1 사이의 소수가 나오게 된다. 0과 1 사이의 소수에 테이블의 크기를 곱해버리면 다시 0과 테이블 크기 사이의 수가 나오게 된다. 즉, 항상 0보다 크거나 같고 테이블 크기인 30보다는 작은 숫자가 나온다. 여기서 소수점 뒷자리를 버리니까 원하는 범위의 자연수를 구할 수 있다.
<br>

### 해시 테이블 <br>

해시 테이블은 이 해시 함수와 배열을 같이 사용하는 자료구조이다. <br>
키를 바로 인덱스로 사용하지 않고 해시 함수에 넣어서 리턴된 값을 인덱스로 사용한다. <br>
즉, 해시 테이블은 고정된 크기의 배열을 만들고 <br>
해시 함수를 이용해서 key를 원하는 범위의 자연수로 바꿔준 후 <br>
해시 함수 결과 값 인덱스에 key - value 쌍을 저장하는 자료 구조이다.

<br>

### 파이썬 hash 함수 <br>

파이썬 언어도 내부적으로 hash라는 함수를 제공한다. 파이썬 해시 함수는 파라미터로 받은 값을 그냥 아무 정수로만 바꿔주는 함수이다.

```python
# 정수 값
print(hash(12345))  # 12345
print(hash(12345))  # 12345

# 다른 정수 값
print(hash(12346))  # 12346

# 소수 값
print(hash(15.1234))  # 284541027336970255
print(hash(15.1234))  # 284541027336970255

# 다른 소수 값
print(hash(81.1234))  # 284541027336978513

# 문자열
print(hash("파이썬"))  # -8002119629611903017
print(hash("파이썬"))  # -8002119629611903017

# 다른 문자열
print(hash("자바"))  # -8553573703343279427
```

이런식으로 같은 값을 넣으면 항상 같은 정수를 리턴해주는 함수이다. 이 때 중요한 점은 hash 함수에 서로 다른 두 값을 파라미터로 넣었을 때 같은 정수가 리턴될 수 없다는 것이다. 데이터를 자신만의 고유한 정수 값으로 바꿔주는 함수다.

파이썬 hash 함수는 언어 자체적으로는 불변 타입 자료형에만 사용할 수 있다. <br>
(불린형, 정수형, 소수형, 튜플, 문자열)
<br><br>

### 해시 테이블 충돌과 Chaining 개념 <br>

**배열 인덱스에 링크드 리스트 저장해서 충돌 해결** <br>

```python
class Node:
    """링크드 리스트의 노드 클래스"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None  # 다음 노드에 대한 레퍼런스
        self.prev = None  # 전 노드에 대한 레퍼런스

class LinkedList:
    """링크드 리스트 클래스"""
    def __init__(self):
        self.head = None  # 링크드 리스트의 가장 앞 노드
        self.tail = None  # 링크드 리스트의 가장 뒤 노드

    # 탐색 메소드
    def find_node_with_key(self, key):
    """링크드 리스트에서 주어진 데이터를 갖고있는 노드를 리턴한다. 단, 해당 노드가 없으면 None을 리턴한다"""
    iterator = self.head   # 링크드 리스트를 돌기 위해 필요한 노드 변수

    while iterator is not None:
        if iterator.key == key:
            return iterator

        iterator = iterator.next

    return None

    # 추가 (맨 뒤 삽입) 메소드
    def append(self, key, value):
    """링크드 리스트 추가 연산 메소드"""
    new_node = Node(key, value)

    # 빈 링크드 리스트라면 head와 tail을 새로 만든 노드로 지정
    if self.head is None:
        self.head = new_node
        self.tail = new_node
    # 이미 노드가 있으면
    else:
        self.tail.next = new_node  # tail의 다음 노드로 추가
        new_node.prev = self.tail
        self.tail = new_node  # tail 업데이트

    # 삭제 메소드
    def delete(self, node_to_delete):
    """더블리 링크드 리스트 삭제 연산 메소드"""

    # 링크드 리스트에서 마지막 남은 데이터를 삭제할 때
    if node_to_delete is self.head and node_to_delete is self.tail:
        self.tail = None
        self.head = None

    # 링크드 리스트 가장 앞 데이터 삭제할 때
    elif node_to_delete is self.head:
        self.head = self.head.next
        self.head.prev = None

    # 링크드 리스트 가장 뒤 데이터 삭제할 떄
    elif node_to_delete is self.tail:
        self.tail = self.tail.prev
        self.tail.next = None

    # 두 노드 사이에 있는 데이터 삭제할 때
    else:
        node_to_delete.prev.next = node_to_delete.next
        node_to_delete.next.prev = node_to_delete.prev

    # 문자열 메소드
    def __str__(self):
    """링크드 리스트를 문자열로 표현해서 리턴하는 메소드"""
    res_str = ""

    # 링크드 리스트 안에 모든 노드를 돌기 위한 변수. 일단 가장 앞 노드로 정의한다.
    iterator = self.head

    # 링크드 리스트 끝까지 돈다
    while iterator is not None:
        # 각 노드의 데이터를 리턴하는 문자열에 더해준다
        res_str += "{}: {}\n".format(iterator.key, iterator.value)
        iterator = iterator.next # 다음 노드로 넘어간다

    return res_str
```

<br>

### Chaining을 쓰는 해시 테이블 연산

<br>

**탐색 연산**

원하는 key에 해당하는 value를 찾는 연산

**탐색 연산 시간 복잡도** <br>

|                    | 탐색 연산 각 단계들 |
| ------------------ | ------------------- |
| 해시 함수 계산     | O(1)                |
| 배열 인덱스 접근   | O(1)                |
| 링크드 리스트 탐색 | O(n)                |
| 총합               | O(n)                |

<br>

**삭제 연산**

특정 key가 주어졌을 때 해시 테이블에서 그 키에 해당하는 key - value 데이터 쌍을 삭제한다.

**삭제 시간 복잡도** <br>

|                         | 탐색 연산 각 단계들 |
| ----------------------- | ------------------- |
| 해시 함수 계산          | O(1)                |
| 배열 인덱스 접근        | O(1)                |
| 링크드 리스트 노드 탐색 | O(n)                |
| 링크드 리스트 노드 삭제 | O(1)                |
| 총합                    | O(n)                |
