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
