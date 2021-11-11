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

<br><br>

### Chaining을 쓰는 해시 테이블 평균 시간 복잡도

<br>

| 동작(Operation) | 시간 복잡도 |
| --------------- | ----------- |
| 탐색 (search)   | O(n)        |
| 저장 (save)     | O(n)        |
| 삭제 (delete)   | O(n)        |

<br>

해시 테이블의 탐색, 저장, 삭제 연산들은 이런 시간 복잡도를 갖는다. <br>
세 연산 모두 key를 이용해서 저장된 링크드 리스트 노드를 탐색하는 과정을 포함한다. <br>
링크드 리스트 탐색 연산은 링크드 리스트의 길이에 비례한다.
<br><br>

**해시 테이블 연산들 분해 분석** <br>

| 연산 (Operation) | 부분 단계들                                                                                                                    | 각 부분 단계 시간 복잡도 |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------ |
| 탐색 (search)    | 1. 해시 함수 계산 <br> 2. 배열 인덱스 접근 <br> 3. 링크드 리스트 탐색                                                          | O(1+1+n)                 |
| 저장 (save)      | 1. 해시 함수 계산 <br> 2. 배열 인덱스 접근 <br> 3. 링크드 리스트 탐색 <br> 4. 탐색한 노드 수정 or 링크드 리스트 앞에 노드 삽입 | O(1+1+n+1)               |
| 삭제 (delete)    | 1. 해시 함수 계산 <br> 2. 배열 인덱스 접근 <br> 3. 링크드 리스트 탐색 <br> 4. 탐색한 노드 삭제                                 | O(1+1+n+1)               |

<br><br>

**배열에 저장되어 있는 링크드 리스트들의 평균 길이** <br>

총 들어있는 key - value 쌍 수를 배열 인덱스 수로 나눠주면 된다. <br>

1. 해시 테이블에 총 들어가 있는 key- value 쌍의 수 : n
2. 해시 테이블이 사용하는 배열의 크기: m

링크드 리스트들의 평균 길이는 $\frac{n}{m}$ 라고 할 수 있다. <br>
링크드 리스트들의 평균 길이가 $\frac{n}{m}$ 이면 각 연산들은 평균적으로 O( $\frac{n}{m}$ ) 이 걸린다 할 수 있다. <br>
해시 테이블을 만들 때 항상 충분히 여유롭게 총 저장하는 key - value 쌍 수와 해시 테이블이 사용하는 배열의 크기를 비슷하거나 작다고 가정을 한다. <br>
즉, 해시 테이블을 사용할 때 항상 어느 정도까지는 n = m 이렇게 유지시켜주는 약속을 하는 것이다. 이 약속만 지켜주면 해시 테이블 연산들이 O($\frac{n}{m}$)이 걸리니까 n = m을 적용하면 다시 O(1)이라고 표현할 수 있다.
<br><br>

**해시 테이블 평균 시간 복잡도 종합**

| 연산 (Operation) | 평균 시간 복잡도 |
| ---------------- | ---------------- |
| 탐색 (search)    | O(1)             |
| 저장 (save)      | O(1)             |
| 삭제 (delete)    | O(1)             |

해시 테이블 삽입, 삭제, 탐색 연산들은 최악의 경우 O(n)이 걸리지만, 평균적으로는 O(1)이 걸린다.

<br><br>

### Open Addressing

Open Addressing은 충돌이 일어났을 때 다른 비어있는 인덱스를 찾아서 거기에 데이터를 저장하는 방법이다. <br>
비어있는 인덱스를 찾는 여러 방법 중 기본적인 방법은 선형 탐사(linear probing)이다. <br>
선형 탐사는 충돌이 일어났을 때, 한 칸씩 다음 인덱스가 비었는지 확인하고 비어있다면 데이터 쌍을 저장한다.

다른 방법으로는 제곱 탐사(Quadratic Probing)가 있다. <br>
제곱 탐사는 처음에 1의 제곱 뒤에 있는 인덱스를 확인하고 차 있다면 차 있는 인덱스에서 2의 제곱 뒤에 있는 인덱스를 확인한다. <br>
이런 방식으로 선형적으로 바로 다음 인덱스들을 하나씩 확인하지 않고, 제곱을 한 값들을 이용해서 인덱스를 찾는다.
<br><br>

**연산들의 세부 단계들**

Chaining과 마찬가지로 key를 해시 함수에 넣어서 삽입하고, 이 결과 값을 이용해서 인덱스에 접근하는 데 걸리는 시간은 O(1)이다. 원하는 인덱스에 key - value 쌍을 저장하는 것도 마찬가지로 O(1)이다. <br>
Open Addressing을 하게 되면 탐색, 삽입, 삭제 연산들 모두 인덱스를 찾는 탐사를 해야 한다. <br>
삽입 연산은 탐사를 통해서 빈 인덱스를 찾고, 탐색과 삭제 연산은 원하는 key를 갖는 데이터 쌍을 찾는다. <br>
탐사 최악의 경우 빈 인덱스를 찾기 위해 배열 안에 있는 모든 인덱스를 하나씩 다 확인해야 하므로 O(n)이 걸린다.
<br><br>

**Open Addressing 연산 시간 복잡도**

| 연산 | 시간 복잡도 (최악의 경우) |
| ---- | ------------------------- |
| 삽입 | O(n)                      |
| 탐색 | O(n)                      |
| 삭제 | O(n)                      |

<br><br>

**Open Addressing을 쓰는 해시 테이블 평균 시간 복잡도**

Load factor <br>

해시 테이블 연산들을 분석할 때는 Load factor라는 것을 사용한다. <br>
Load factor α는 해시 테이블이 사용하는 배열의 크기를 m, 해시 테이블 안에 들어있는 데이터 쌍 수를 n이라고 할 때: α = $\frac{n}{m}$ 이다. 해시 테이블이 얼마나 차있는지를 나타내는 변수이다. <br>
Open Addressing을 할 때 해시 테이블의 연산들을 분석할 때는 Load factor는 굉장히 중요한 역할을 한다. <br>
해시 테이블 안에 배열의 크기보다 많은 key - value 쌍을 저장할 수 없기 때문에 Load factor α는 항상 1보다 작다고 가정한다.

**결과**

결과적으로 얘기하면 Open addressing을 사용하는 해시 테이블에서 평균적으로 탐사를 해야 되는 횟수 (기댓값)은 $\frac{1}{1-α}$ 보다 작다.

| 연산 | 시간 복잡도 (평균) |
| ---- | ------------------ |
| 삽입 | O(1)               |
| 탐색 | O(1)               |
| 삭제 | O(1)               |
