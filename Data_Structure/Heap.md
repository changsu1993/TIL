# 1. Heap (힙)

**조건**

- 형태 속성: 힙은 완전 이진 트리다.
- 힙 속성: 모든 노드의 데이터는 자식 노드들의 데이터보다 크거나 같다.

<br>

### 정렬

정렬이란 여러 개의 데이터 요소들을 특정 순서로 배치하는 것을 말한다.

```python
# 파이썬 리스트
[4, 1, 6, 2, 8, 5]

# 오름차순 정렬
[1, 2, 4, 5, 6, 8]

# 내림차순 정렬
[8, 6, 5, 4, 2, 1]
```

정렬 알고리즘: 데이터를 재배치하는 구체적인 방법

가장 흔한 정렬 알고리즘들 중에서는 삽입 정렬, 선택 정렬, 퀵 정렬, 합병 정렬 등이 있다.

<br>

**배열로 구현한 힙**

힙은 완전 이진 트리이기 때문에 보통 동적 배열로 나타낸다. <br>

<br>

**힙 만들기**

힙을 만들기 위해서는 형태 속성과 힙 속성의 조건을 만족해야 한다. <br>
힙 속성이 지켜지지 않을 때에는 heapify 알고리즘을 통해 해결할 수 있다. <br>
heapify는 파라미터로 어떤 노드 하나를 받는다. 이 노드를 부모 노드로 지정하고 <br>
부모 노드, 왼쪽 자식, 오른쪽 자식 중 가장 큰 걸 고른다. <br>
가장 큰 노드가 부모 노드가 아니라면 가장 큰 노드와 부모 노드를 바꿔준다. <br>
부모 노드가 가장 크면 아무것도 하지 않고, 기존의 부모 노드가 밑으로 갔다면 또 힙 속성을 어길 수도 있다. <br>
이럴 경우 힙 속성이 충족될 때까지 반복한다. <br>
heapify 알고리즘을 쓰면 원하는 노드를 힙 속성에 맞는 위치로 재배치 시킬 수 있다. <br>

시간 복잡도 <br>
트리에 저장되어 있는 노드의 개수를 n이라 하고, <br>
최악의 경우 <br>
이 노드는 총 트리의 높이만큼 데이터를 비교하고 재배치 시킨다. 힙은 완전 이진 트리이기 때문에 높이가 O(log(n))이다. <br>
따라서 최악의 경우 heapify에 걸리는 시간은 O(log(n))에 비례한다. 그렇기 때문에 시간 복잡도도 O(log(n))이다. <br>
힙을 만들려면 heapify를 n개의 노드에 모두 호출해야 하므로 O(log(n))이 n번 걸린다. <br>
log(n) x n = n log(n) 이므로 힙을 만드는 데 걸리는 시간 복잡도는 O(n log(n))이다.

<br>

**힙 정렬**

힙을 이용한 정렬 알고리즘

- 힙을 만든다.
- root와 마지막 노드를 바꿔준다.(바꾼 노드는 없는 노드 취급한다.)
- 새로운 노드가 힙 속성을 지킬 수 있게 heapify 호출한다.
- 힙에 남아있는 노드가 없도록 단계 2 ~ 3을 반복한다.

1번째 단계인 리스트를 힙으로 만드는 데 걸리는 시간은 O(n log(n))이다. <br>
2번째 단계는 그냥 두 노드의 위치를 바꿔 주는 작업이기 때문에 노드의 개수 n과는 상관없이 항상 O(1)이다. <br>
3번째 단계는 새로운 root 노드에 heapify를 하니까 시간 복잡도는 O(log(n))이다. 2번째 단계와 3번째 단계를 합치면 O(log(n)+1) 즉, O(log(n))이다. <br>
4번째 단계는 2~3 단계를 반복한다. 힙에는 총 n개의 노드가 있으므로 2, 3, 4단계의 시간 복잡도를 종합하면 O(n log(n))이다. <br>

정리하면

- 힙을 만드는 데 O(n log(n))
- 만든 힙에서 매번 root 노드를 뽑고 남은 것들을 다시 힙으로 만들어주는 작업을 반복하는 데 O(n log(n))이 걸린다.

그럼 힙 정렬의 총 시간 복잡도는 O(n log(n)+n log(n))으로 O(2n log(n))이고, 시간 복잡도에서 상수는 무시되니까 결국 O(n log(n))이라고 할 수 있다. <br>
힙 정렬은 O(n log(n))의 시간 복잡도를 가지는 정렬 알고리즘인 것이다.

<br>

**다른 정렬 알고리즘들과의 비교**

| 정렬 알고리즘 | 시간 복잡도                        |
| ------------- | ---------------------------------- |
| 선택 정렬     | $O(n^2)$                           |
| 삽입 정렬     | $O(n^2)$                           |
| 합병 정렬     | $O(n log(n))$                      |
| 퀵 정렬       | 평균 $O(n log(n))$ (최악 $O(n^2)$) |
| 힙 정렬       | $O(n log(n))$                      |

힙 정렬은 선택 정렬과 삽입 정렬 ($O(n^2)$)보다는 좋고, 합병 정렬과 퀵 정렬 ($O(n log(n))$)과는 비슷한 성능을 내는 정렬 방법이다.

<br>

**우선순위 큐**

힙은 우선순위 큐 추상 자료형을 효율적으로 구현할 수 있다. <br>
우선순위 큐는 큐나 스택처럼 추상 자료형이다.

- 데이터를 저장할 수 있다.
- 저장한 데이터가 우선순위 순서대로 나온다.

<br>

**힙에 데이터 삽입하기** <br>

- 힙의 마지막 인덱스에 데이터를 삽입한다.
- 삽입한 데이터와 부모 노드의 데이터를 비교한다.
- 부모 노드의 데이터가 더 작으면 둘의 위치를 바꿔준다.

```python
def swap(tree, index_1, index_2):
    """완전 이진 트리의 노드 index_1과 노드 index_2의 위치를 바꿔준다"""
    temp = tree[index_1]
    tree[index_1] = tree[index_2]
    tree[index_2] = temp


def reverse_heapify(tree, index):
    """삽입된 노드를 힙 속성을 지키는 위치로 이동시키는 함수"""
    parent_index = index // 2  # 삽입된 노드의 부모 노드의 인덱스 계산
    # 코드를 쓰세요.
    if 0 < parent_index < len(tree) and tree[parent_index] < tree[index]:
        swap(tree, index, parent_index)
        reverse_heapify(tree, parent_index)

class PriorityQueue:
    """힙으로 구현한 우선순위 큐"""
    def __init__(self):
        self.heap = [None]  # 파이썬 리스트로 구현한 힙


    def insert(self, data):
        """삽입 메소드"""
        # 코드를 쓰세요
        self.heap.append(data)
        reverse_heapify(self.heap, len(self.heap)-1)

    def __str__(self):
        return str(self.heap)


# 실행 코드
priority_queue = PriorityQueue()

priority_queue.insert(6)
priority_queue.insert(9)
priority_queue.insert(1)
priority_queue.insert(3)
priority_queue.insert(10)
priority_queue.insert(11)
priority_queue.insert(13)

print(priority_queue)
```

<br>

**힙에서 최고 우선순위 데이터 추출하기**

- root 노드와 마지막 노드를 서로 바꿔준다.
- 마지막 노드의 데이터를 변수에 저장해 준다.
- 마지막 노드를 삭제한다.
- root 노드에 heapify를 호출해서 망가진 힙 속성을 고친다.
- 변수에 저장한 데이터를 리턴한다. (최고 우선순위 데이터)

```python
from heapify_code import *

class PriorityQueue:
    """힙으로 구현한 우선순위 큐"""
    def __init__(self):
        self.heap = [None]  # 파이썬 리스트로 구현한 힙

    def insert(self, data):
        """삽입 메소드"""
        self.heap.append(data)  # 힙의 마지막에 데이터 추가
        reverse_heapify(self.heap, len(self.heap)-1) # 삽입된 노드(추가된 데이터)의 위치를 재배치

    def extract_max(self):
        """최우선순위 데이터 추출 메소드"""
        # 코드를 쓰세요
        swap(self.heap, 1, len(self.heap)-1)
        max_value = self.heap.pop()
        heapify(self.heap, 1, len(self.heap))
        return max_value


    def __str__(self):
        return str(self.heap)

# 출력 코드
priority_queue = PriorityQueue()

priority_queue.insert(6)
priority_queue.insert(9)
priority_queue.insert(1)
priority_queue.insert(3)
priority_queue.insert(10)
priority_queue.insert(11)
priority_queue.insert(13)

print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
print(priority_queue.extract_max())
```

<br>

**힙의 삽입 연산 시간 복잡도**

힙 안에 총 n개의 노드가 있다고 가정하고 데이터 삽입의 3단계 <br>

1. 힙의 마지막 인덱스에 노드를 삽입한다.
2. (1) 삽입한 노드와 그 부모 노드를 비교해서 부모 노드가 더 작다면 둘의 위치를 바꾼다. <br> (2) 삽입한 노드와 그 부모 노드를 비교해서 부모 노드가 더 크면 그대로 둔다.
3. 2-1의 경우에는 삽입한 노드가 올바른 위치를 찾을 때까지 단계 2를 반복한다.

<br>

1단계

먼저 힙의 마지막에 노드를 삽입해야 한다. 동적 배열에 원소를 추가하는 것의 시간 복잡도를 분할 상환 분석하면 O(1)이다.

2단계

(1) 삽입된 노드의 값과 부모 노드의 값을 비교하는 건 O(1)이 걸린다. <br>
(2) 삽입된 데이터가 더 큰 경우 부모 노드와의 위치를 바꿔주는 것도 마찬가지로 O(1)이 걸린다.

3단계

최악의 경우는 삽입한 데이터가 leaf 노드부터 시작해서 root 노드까지 올라가는 경우이다. <br>
그럼 힙의 높이만큼 2단계를 반복해야 한다. 힙의 높이는 log(n)에 비례하므로 시간은 O(log(n))이다.<br>

- 1단계의 O(1)
- 2단계, 3단계의 O(log(n))

더하면 O(1+log(n)), 결국 시간 복잡도는 O(log(n))이 걸린다.

<br>

**힙의 추출 연산 시간 복잡도**

힙에 있는 노드의 개수를 n이라고 가정하고 4단계 <br>

1. root 노드와 마지막 노드의 위치를 바꾼다.
2. 마지막 위치로 간 원래 root 노드의 데이터를 별도 변수에 저장하고, 노드는 힙에서 지운다.
3. 새로운 root 노드를 대상으로 heapify해서 망가진 힙 속성을 복원한다.
4. 2단계에서 따로 저장해 둔 최우선순위 데이터를 리턴한다.

<br>

1단계

root 노드와 마지막 노드의 위치를 바꾸는 건 노드의 개수랑은 전혀 상관없이 O(1)이 걸린다.

2단계

데이터를 변수에 지정하는 건 O(1)이 걸린다. 동적 배열에서 마지막 인덱스의 원소를 삭제하는 건 분할 상환 분석을 하면 O(1)이 걸린다. O(1+1)은 O(1)

3단계

새로운 root 노드를 대상으로 heapify를 호출해서 망가진 힙 속성을 복원하는 단계이다. O(log(n))

4단계

변수를 리턴하는 건 한 번에 할 수 있다. O(1) <br>
총 걸리는 시간을 더하면 O(1+1+log(n)+1) <br>
힙에서 가장 우선 순위가 높은 데이터를 추출하는 연산의 시간 복잡도는 O(log(n))이다.

<br>

**힙으로 구현한 우선순위 큐 평가**

우선순위 큐를 구현할 때는 힙 말고도 다른 자료 구조들을 활용할 수도 있다.

- 정렬된 동적 배열
- 정렬된 더블리 링크드 리스트

<br>

**정렬된 동적 배열**

데이터를 삽입하거나 추출해도 동적 배열이 늘 정렬된 상태를 유지하게 하면 된다. <br>
동적 배열에 데이터가 정렬된 채(오름차순 또는 내림차순)로 있다고 가정하고 새로운 데이터를 삽입한다면 크게 두 가지 작업을 해야한다. <br>
(1) 먼저 새로운 데이터가 어느 위치에 들어가야 하는지를 찾고
(2) 그 위치에 데이터를 넣어야 한다.

- 삽입할 위치를 찾는 것은 이진 탐색을 사용하면 O(log(n))이 걸린다.
- 그리고 그 위치에 데이터를 삽입하는 건 최악의 경우 O(n)이 걸린다.

그럼 삽입 연산은 총 O(log(n)+n)이 걸리고 결국, 정렬된 동적 배열에 데이터를 삽입하는 연산은 O(n)이 걸린다. <br>
정렬된 동적 배열에서 가장 우선순위가 높은 데이터를 추출하는 연산은 O(1)이 걸린다.

<br>

**정렬된 더블리 링크드 리스트**

링크드 리스트에서는 데이터를 삽입해야 하는 위치를 찾을 때 선형 탐색을 해야 한다. <br>
총 노드 수가 n이라고 했을 때, 최악의 경우 n개의 노드를 다 봐야 한다. <br>
삽입할 위치를 찾는 단계는 O(n)이 걸리고 삽입과 추출은 O(1)이 걸린다.

<br>

|                             | 데이터 삽입 | 데이터 추출 |
| --------------------------- | ----------- | ----------- |
| 정렬된 동적 배열            | O(n)        | O(1)        |
| 정렬된 더블리 링크드 리스트 | O(n)        | O(1)        |
| 힙                          | O(log(n))   | O(log(n)))  |

<br>

우선순위를 사용할 때

- 정렬된 동적 배열이나 정렬된 더블리 링크드 리스트를 사용하면 데이터를 추출할 때 더 효율적
- 힙을 사용하면 데이터를 삽입할 때 더 효율적
