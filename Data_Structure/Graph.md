# 1. Graph (그래프)

그래프는 연결 관계가 있는 데이터를 저장하는 자료 구조이다.

ex) 위치 데이터 (지하철 앱, 네비게이션) <br>
ex) 사회 연결망 (페이스북, 인스타그램)

다양한 연결 관계

- 통신: 수많은 컴퓨터들의 연결 관계인 인터넷
- 생물: 유전자와 단백질의 상호 작용 관계

<br><br>

### **그래프 기본**

그래프는 노드라는 기본적인 단위를 사용하고 노드들 사이에 있는 관계를 엣지라고 한다.
<br><br>

### **그래프 용어/성질 정리**

노드: 그래프에서 하나의 데이터 단위를 나타내는 객체 (SNS 그래프에서는 하나의 유저가 하나의 노드이다.) <br>

엣지: 그래프에서 두 노드의 직접적인 연결 관계 데이터 (페이스북 유저 그래프에서는 두 유저의 친구 관계에 해당하는 데이터) 엣지가 갖는 특성에 따라 그래프의 종류가 나뉘기도 한다. <br>

- 방향 그래프(directed graph): 방향 그래프에서는 엣지들이 방향을 갖는다. <br> 인스타그램의 팔로우 관계처럼 한 유저가 다른 유저를 팔로우하는 일방적인 관계를 나타낼 수 있게 해준다.
- 가중치 그래프(weighted graph): 가중치 그래프에서는 엣지들이 연결 관계뿐만 아니라 어떤 정보를 나타내는 수치를 가진다. 정보의 예) 위치 정보 그래프면 두 장소 사이의 거리 등

차수: 하나의 노드에 연결된 엣지들의 수 <br>

- 무방향 그래프에서는 하나의 노드에 연결된 엣지들의 수를 나타내고, 방향 그래프에서는 노드를 떠나는 엣지의 수를 출력 차수, 노드에 들어오는 엣지의 수를 입력 차수로 구별해서 부른다.

경로: 한 노드에서 다른 노드까지 가는 길

- 경로의 거리
  - 비가중치 그래프: 한 경로에 있는 엣지의 수
  - 가중치 그래프: 한 경로에 있는 엣지의 가중치의 합
- 최단 경로: 두 노드 사이의 경로 중 거리가 가장 짧은 경로
- 사이클: 한 노드에서 시작해서 같은 노드로 돌아오는 경로

<br><br>

### **그래프 노드 구현**

```python
class StationNode:
    """지하철 역 노드를 나타내는 클래스"""
    def __init__(self, name, num_exits):
        self.name = name
        self.num_exits = num_exits


# 지하철 역 노드 인스턴스 생성
station_0 = StationNode("서울역", 16)
station_1 = StationNode("종로3가역", 16)
station_2 = StationNode("사당역", 14)
station_3 = StationNode("교대역", 14)

# 노드들을 파이썬 리스트에 저장
stations = [station_0, station_1, station_2, station_3]

# 지하철 역 노드들을 파이썬 딕셔너리에 저장
stations = {
    "서울역": station_0,
    "종로3가역": station_1,
    "사당역": station_2,
    "교대역": station_3
}

node_1 = stations["서울역"]
node_2 = stations["종로3가역"]
```

<br><br>

### **그래프 엣지 구현**

**인접 행렬**

- 노드들의 연결 관계(엣지)를 나타내는 2차원 리스트
- 각 노드를 리스트에 저장해 고유 정수 인덱스를 준다.
- 노드 수 X 노드 수 크기의 행렬을 만든다.
- 노드들의 엣지 유무 및 가중치에 따라 행렬의 요소를 채운다.

```python
# 모든 요소를 0으로 초기화시킨 크기 6 x 6 인접 행렬
adjacency_matrix = [[0 for i in range(6)] for i in range(6)]


# 엣지 (영훈, 현승) 저장
adjacency_matrix[0][1] = 1
adjacency_matrix[1][0] = 1

# 엣지 (영훈, 동욱) 저장
adjacency_matrix[0][2] = 1
adjacency_matrix[2][0] = 1

# 엣지 (현승, 소원) 저장
adjacency_matrix[1][5] = 1
adjacency_matrix[5][1] = 1

# 엣지 (현승, 지웅) 저장
adjacency_matrix[1][3] = 1
adjacency_matrix[3][1] = 1

# 엣지 (동욱, 소원) 저장
adjacency_matrix[2][5] = 1
adjacency_matrix[5][2] = 1

# 엣지 (지웅, 소원) 저장
adjacency_matrix[3][5] = 1
adjacency_matrix[5][3] = 1

# 엣지 (지웅, 규리) 저장
adjacency_matrix[3][4] = 1
adjacency_matrix[4][3] = 1

# 엣지 (규리, 소원) 저장
adjacency_matrix[4][5] = 1
adjacency_matrix[5][4] = 1

print(adjacency_matrix)
```

<br><br>

**인접 리스트**

- 각 노드의 엣지를 리스트에 저장하는 방법

```python
class StationNode:
    """간단한 지하철 역 노드 클래스"""
    def __init__(self, station_name):
        self.station_name = station_name
        self.adjacent_stations = []  # 인접 리스트


    def add_connection(self, other_station):
        """지하철 역 노드 사이 엣지 저장하기"""
        self.adjacent_stations.append(other_station)
        other_station.adjacent_stations.append(self)


    def __str__(self):
        """지하철 노드 문자열 메소드. 지하철 역 이름과 연결된 역들을 모두 출력해준다"""
        res_str = f"{self.station_name}: "  # 리턴할 문자열

        # 리턴할 문자열에 인접한 역 이름들 저장
        for station in self.adjacent_stations:
            res_str += f"{station.station_name} "

        return res_str
```

```python
from StationNode import *

def create_subway_graph(input_file):
    """input_file에서 데이터를 읽어 와서 지하철 그래프를 리턴하는 함수"""
    stations = {}  # 지하철 역 노드들을 담을 딕셔너리

    # 파라미터로 받은 input_file 파일을 연다
    with open(input_file) as stations_raw_file:
        for line in stations_raw_file:  # 파일을 한 줄씩 받아온다
            previous_station = None # 엣지를 저장하기 위한 도우미 변수. 현재 보고 있는 역 전 역을 저장한다.
            subway_line = line.strip().split("-")  # 앞 뒤 띄어쓰기를 없애고 "-"를 기준점으로 데이터를 나눈다

            for name in subway_line:
                station_name = name.strip()  # 앞 뒤 띄어쓰기 없애기

                # 지하철 역 이름이 이미 저장한 key 인지 확인
                if station_name not in stations:
                    current_station = StationNode(station_name)  # 새로운 인스턴스를 생성하고
                    stations[station_name] = current_station  # dictionary에 역 이름은 key로, 역 노드 인스턴스를 value로 저장한다

                else:
                    current_station = stations[station_name] # 이미 저장한 역이면 stations에서 역 인스턴스를 갖고 온다

                if previous_station is not None:
                    current_station.add_connection(previous_station) # 현재 역과 전 역의 엣지를 연결한다

                previous_station = current_station # 현재 역을 전 역으로 저장


    return stations


stations = create_subway_graph("./stations.txt")  # stations.txt 파일로 그래프를 만든다

# stations에 저장한 역 인접 역들 출력 (채점을 위해 역 이름 순서대로 출력)
for station in sorted(stations.keys()):
        print(stations[station])
```

<br><br>

### **인접 행렬 vs 인접 리스트**

<br>

**복잡도 표현 기호**

V(Vertex) : 그래프 안에 있는 모든 노드들의 집합이다. <br>
E(Edge): 그래프 안에 있는 모든 엣지들의 집합이다. <br><br>
노드 수가 V일 때 그래프 안에 최대 엣지의 수는 무방향 그래프는 $\frac{V^2}{2}$ , 방향 그래프는 $V^2$ 개의 엣지를 갖는다. E는 최악의 경우 $V^2$ 에 비례한다.

<br>

**노드를 저장하는 공간**

인접 행렬을 사용하던 인접 리스트를 사용하던 노드들을 저장해야 된다. <br>
총 V개의 노드를 저장하기 때문에 노드를 저장하는 데는 O(V)의 공간을 사용한다고 할 수 있다.

<br>

**인접 행렬이 차지하는 공간**

인접 행렬 정의는 "총 노드의 수 X 총 노드의 수" <br>
그래프 안에 있는 노드의 수가 V라고 할 때 인접 행렬은 V \* V 크기의 행렬을 저장하고 각 요소들이 0 또는 1을 저장한다. <br>
그렇기 때문에 인접 행렬은 총 $V^2$ 에 비례하는 공간, $O(V^2)$ 의 공간을 사용한다.

<br>

**인접 리스트가 차지하는 공간**

인접 리스트는 각 노드가 자신과 인접한 노드들을 가리키는 레퍼런스를 저장하고 있다. <br>
모든 노드는 하나의 인접 리스트를 갖기 때문에 최소 $O(V)$ 만큼의 공간을 차지한다. <br>
엣지를 저장하는 공간은 무방향 그래프 일 때 $2E$ , 방향 그래프일 때는 $E$ 이다. <br>
총 저장하는 레퍼런스 수는 $E$ 에 비례한다고 할 수 있다. $O(E)$ <br>
이걸 합치면 인접 리스트 자체를 저장하는데 $O(V)$ , 엣지를 저장하는데 $O(E)$ 를 사용하기 때문에 총 $O(V+E)$ 만큼의 공간을 사용한다고 표현한다.

<br>

**두 노드가 연결됐는지 확인하는 데 걸리는 시간**

인접 행렬을 이용하면 두 노드가 인접했는지 아닌지를 $O(1)$ 으로 알아낼 수 있다. (adjacency_matrix[1][2])<br>
인접 리스트는 한 노드의 리스트 안에 특정 역이 저장됐는지를 탐색해야 되는데 선형 탐색을 해야되기 때문에 리스트 안에 있는 데이터를 다 돌아야 한다. <br>
몇 개의 데이터가 있는지에 따라 다르지만 최악의 경우 V개의 요소를 확인해야 한다. <br>

```python
gangnam_station = stations["강남"]
seocho_station = stations["서초"]

print(seocho_station in gangnam_station.adjacent_stations)
```

<br>

**한 노드에 연결된 모든 노드들을 알아내는데 걸리는 시간**

인접 행렬에서는 한 노드를 나타내는 배열, 또는 파이썬 리스트 전체를 다 돌아야지만 그 노드가 연결된 다른 노드들을 갖고 올 수 있다. <br>
모든 리스트 안에는 총 V개의 데이터 요소가 들어 있으니까 매번 V번 돌아야 한다. <br>

인접 리스트를 쓸 때는 각 노드가 자신과 인접한 노드들에 대한 레퍼런스만 갖고 있다. <br>
최악의 경우 한 노드가 다른 모든 노드들과 연결돼 있으면 인접 행렬과 마찬가지로 총 V번 돌아서 인접한 노드들을 가지고 와야 하지만 대부분의 경우 인접 행렬을 사용하는 거보다 더 빨리 실행된다.

<br><br>

## 그래프 탐색

하나의 시작점 노드에서 연결된 노드들을 모두 찾는 것을 말한다. <br>
그래프 탐색 알고리즘은 각 노드들을 어떤 순서로 탐색하는지에 따라

- Breadth First Search
- Depth First Search

두 종류로 나뉜다.

<br>

### Breadth First Search(BFS)

<br>

그래프를 너비 우선적으로 탐색한다.

<br>

**알고리즘**

- 시작 노드를 방문 표시 후, 큐에 넣는다
- 큐에 아무 노드가 없을 때까지:
  - 큐 가장 앞 노드를 꺼낸다
  - 꺼낸 노드에 인접한 노드들을 모두 보면서:
    - 처음 방문한 노드면:
      - 방문한 노드 표시를 해준다
      - 큐에 넣어준다

```python
class StationNode:
    """지하철 역을 나타내는 역"""
    def __init__(self, station_name):
        self.station_name = station_name
        self.adjacent_stations = []
        self.visited = False

    def add_connection(self, station):
        """파라미터로 받은 역과 엣지를 만들어주는 메소드"""
        self.adjacent_stations.append(station)
        station.adjacent_stations.append(self)


def create_station_graph(input_file):
    stations = {}

    # 일반 텍스트 파일을 여는 코드
    with open(input_file) as stations_raw_file:
        for line in stations_raw_file:  # 파일을 한 줄씩 받아온다
            previous_station = None  # 엣지를 저장하기 위한 변수
            raw_data = line.strip().split("-")

            for name in raw_data:
                station_name = name.strip()

                if station_name not in stations:
                    current_station = StationNode(station_name)
                    stations[station_name] = current_station

                else:
                    current_station = stations[station_name]

                if previous_station is not None:
                    current_station.add_connection(previous_station)

                previous_station = current_station

    return stations
```

```python
from collections import deque
from subway_graph import create_station_graph

def bfs(graph, start_node):
    """시작 노드에서 bfs를 실행하는 함수"""
    queue = deque()  # 빈 큐 생성

    # 일단 모든 노드를 방문하지 않은 노드로 표시
    for station_node in graph.values():
        station_node.visited = False

    # 시작점 노드를 방문 표시한 후 큐에 넣어준다.
    start_node.visited = True
    queue.append(start_node)

    while queue:  # 큐에 노드가 있는 동안
        current_station = queue.popleft()  # 큐의 가장 앞 데이터를 갖고 온다
        for neighbor in current_station.adjacent_stations:  # 인접한 노드를 돌면서
            if not neighbor.visited:  # 방문하지 않은 노드면
                neighbor.visited = True  # 방문 표시를 하고
                queue.append(neighbor)  # 큐에 넣는다


stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

gangnam_station = stations["강남"]

# 강남역과 경로를 통해 연결된 모든 노드를 탐색
bfs(stations, gangnam_station)

# 강남역과 서울 지하철 역들이 연결됐는지 확인
print(stations["강동구청"].visited)
print(stations["평촌"].visited)
print(stations["송도"].visited)
print(stations["개화산"].visited)

# 강남역과 대전 지하철 역들이 연결됐는지 확인
print(stations["반석"].visited)
print(stations["지족"].visited)
print(stations["노은"].visited)
print(stations["(대전)신흥"].visited)
```

<br><br>

### BFS 알고리즘 시간 복잡도

<br>

총 노드의 수를 V, 엣지의 수를 E

<br>

**BFS 노드 전처리**

모든 노드를 다 돌면서 방문했다는 노드 표시인 visited 변수를 False로 만들어야 하기 때문에 노드들 전처리는 $O(V)$ 가 걸린다고 할 수 있다.

<br>

**큐에 노드를 넣고 빼는 데 걸리는 시간**

BFS는 방문한 노드를 표시하고 다시 방문하지 않는다. <br>
큐는 더블리 링크드 리스트를 사용하면 맨 뒤에 삽입하고 맨 앞에 있는 데이터를 꺼내오는 연산들을 $O(1)$ 으로 할 수 있다. <br>
최대 V개의 노드들이 큐에 들어갔다 나오므로 걸리는 총 시간은 $O(V)$ 라고 할 수 있다.

<br>

**큐에서 뺀 노드의 인접한 노드들을 도는데 걸리는 시간**

노드가 한 번 나올 때마다 그 노드의 인접 리스트도 딱 한번만 돌기 때문에 E에 비례하는 만큼 실행된다고 할 수 있다. <br>
큐에서 뺀 노드들의 인접한 노드들을 도는데 $O(E)$ 가 걸린다.

<br>

**정리**

전처리: $O(V)$ <br>
큐에서 노드 넣고 빼기: $O(V)$ <br>
인접한 노드들을 도는데 걸리는 시간: $O(E)$ <br>
총 $O(V+E)$ 의 시간 복잡도가 걸린다고 할 수 있다.

<br><br>

### Depth First Search(DFS)

<br>

그래프를 깊이 우선적으로 탐색한다.

<br>

**알고리즘**

- 시작 노드를 옅은 회색 표시 후, 스택에 넣는다
- 스택에 아무 노드가 없을 때까지:
  - 스택 가장 위 노드를 꺼낸다
  - 노드를 방문(진한 회색) 표시한다
  - 인접한 노드들을 모두 보면서:
    - 처음 방문하거나 스택에 없는 노드면:
      - 옅은 회색 표시를 해준다
      - 스택에 넣어준다

```python
from collections import deque
from subway_graph import *

def dfs(graph, start_node):
    """dfs 함수"""
    stack = deque()  # 빈 스택 생성

    # 모든 노드를 처음 보는 노드로 초기화
    for station_node in graph.values():
        station_node.visited = 0

    # 시작 노드를 스택에 넣는다는 표시(옅은 회색)를 하고
    start_node.visited = 1
    stack.append(start_node)  # 스택에 넣는다

    while stack:  # 스택에 노드가 남아 있을 때까지
        current_node = stack.pop()  # 스택 가장 위(뒤) 노드를 갖고 온다
        current_node.visited = 2  # 현재 노드를 방문 표시한다
        for neighbor in current_node.adjacent_stations:
            if neighbor.visited == 0:  # 처음 보는 노드들만
                neighbor.visited = 1  # 스택에 넣는다는 표시를 하고
                stack.append(neighbor)  # 스택에 넣는다


stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

gangnam_station = stations["강남"]

# 강남역과 경로를 통해 연결된 모든 노드를 탐색
dfs(stations, gangnam_station)

# 강남역과 서울 지하철 역들 연결됐는지 확인
print(stations["강동구청"].visited)
print(stations["평촌"].visited)
print(stations["송도"].visited)
print(stations["개화산"].visited)

# 강남역과 대전 지하철 역들 연결됐는지 확인
print(stations["반석"].visited)
print(stations["지족"].visited)
print(stations["노은"].visited)
print(stations["(대전)신흥"].visited)
```

<br><br>

### DFS 알고리즘 시간 복잡도

<br>

총 노드의 수를 V, 엣지의 수를 E

<br>

**DFS 노드 전처리**

모든 노드를 노란색 노드로 표시하는 데는 V의 시간이 걸린다. <br>
노드들 전처리는 $O(V)$ 가 걸린다고 할 수 있다.

<br>

**스택에 노드를 넣고 빼는 데 걸리는 시간**

DFS를 할 때도 스택에 같은 노드가 두 번 들어갈 수 없다. <br>
스택은 더블리 링크드 리스트를 사용하면 맨 뒤에 삽입하고 맨 뒤에 있는 데이터를 꺼내오는 연산들을 $O(1)$ 으로 할 수 있다. <br>
최대 V개의 노드들이 스택에 들어갔다 나오므로 노드들이 스택에 들어갔다 나오는 데 걸리는 총 시간은 $O(V)$ 라고 할 수 있다.

<br>

**스택에서 뺀 노드들의 인접한 노드들을 도는데 걸리는 시간**

모든 노드는 스택에 한 번만 들어가서 한 번만 나올수 있기 때문에 모든 노드들의 인접 리스트를 딱 한 번만 돈다고 할 수 있다. <br>
총 엣지 수가 E니까 이 단계도 총 E에 비례하는 만큼 실행된다고 할 수 있다. <br>
스택에서 뺀 노드들의 인접한 노드들을 도는데 $O(E)$ 가 걸린다.

<br>

**장리**

전처리: $O(V)$ <br>
스택에서 노드 넣고 빼기: $O(V)$ <br>
인접한 노드들을 도는데 걸리는 시간: $O(E)$ <br>
총 $O(V+E)$ 의 시간 복잡도가 걸린다고 할 수 있다.

<br><br>

## 최단 경로 알고리즘 (Shortest Path)

 <br>

두 노드 사이 경로 중 가장 거리가 짧은 경로이다.

<br><br>

### BFS predecessor

- 시작 노드를 방문 표시 후, 큐에 넣는다
- 큐에 아무 노드가 없을 때까지:
  - 큐 가장 앞 노드를 꺼낸다
  - 꺼낸 노드에 인접한 노드들을 모두 보면서:
    - 처음 방문한 노드면:
      - 방문한 노드 표시를 해준다
      - predecessor 변수를 큐에서 꺼낸 노드로 설정
      - 큐에 넣어준다

<br>

**Backtracking**

- 현재 노드를 경로에 추가한다
- 현재 노드의 predecessor로 간다
- predecessor가 없을 때까지 위 단계들 반복

<br>

BFS를 하고 난 후에 도착 노드에서부터 Backtracking을 하면 시작점에서 도착점까지의 최단 경로를 구할 수 있다.

```python
from collections import deque
from subway_graph import *

def bfs(graph, start_node):
    """최단 경로용 bfs 함수"""
    queue = deque()  # 빈 큐 생성

    # 모든 노드를 방문하지 않은 노드로 표시, 모든 predecessor는 None으로 초기화
    for station_node in graph.values():
        station_node.visited = False
        station_node.predecessor = None

    # 시작점 노드를 방문 표시한 후 큐에 넣어준다
    start_node.visited = True
    queue.append(start_node)

    while queue:  # 큐에 노드가 있을 때까지
        current_station = queue.popleft()  # 큐의 가장 앞 데이터를 갖고 온다
        for neighbor in current_station.adjacent_stations:  # 인접한 노드를 돌면서
            if not neighbor.visited:  # 방문하지 않은 노드면
                neighbor.visited = True  # 방문 표시를 하고
                neighbor.predecessor = current_station  # 이 노드가 어디서 왔는지 표시
                queue.append(neighbor)  # 큐에 넣는다


def back_track(destination_node):
    """최단 경로를 찾기 위한 back tracking 함수"""
    res_str = ""  # 리턴할 결과 문자열
    temp = destination_node  # 도착 노드에서 시작 노드까지 찾아가는 데 사용할 변수

    # 시작 노드까지 갈 때까지
    while temp is not None:
        res_str = f"{temp.station_name} {res_str}"  # 결과 문자열에 역 이름을 더하고
        temp = temp.predecessor  # temp를 다음 노드로 바꿔준다

    return res_str

stations = create_station_graph("./new_stations.txt")  # stations.txt 파일로 그래프를 만든다

bfs(stations, stations["을지로3가"])  # 지하철 그래프에서 을지로3가역을 시작 노드로 bfs 실행
print(back_track(stations["강동구청"]))  # 을지로3가에서 강동구청역까지 최단 경로 출력
```

<br><br>

### Dijkstra 알고리즘 (가중치 그래프 최단 경로)

Dijkstra 알고리즘을 사용하기 위해서는 그래프 노드에 3가지 변수를 저장해야 한다. <br>

1. distance <br>
   특정 노드까지의 "최단 거리 예상치" (현재까지 아는 정보로 계산한 최단 거리)
2. predecessor <br>
   현재까지 최단 경로에서 바로 직전의 노드
3. complete <br>
   노드까지의 최단 경로를 찾았다고 표시하기 위한 변수

<br>

**엣지 Relaxation**

A에서 B를 방문하면서 B의 distance, predecessor을 바꾸는 것

<br>

**일반화**

- 시작점의 distance를 0으로, predecessor를 None으로
- 모든 노드가 complete 일 때까지:
  - complete하지 않은 노드 중 distance가 가장 작은 노드 선택
  - 이 노드에 인접한 노드 중 complete하지 않은 노드를 돌면서:
    - 각 엣지를 relax 한다
  - 현재 노드를 complete 처리한다
