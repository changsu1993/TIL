# 1. List (리스트)

변수에 값을 여러 개 저장할 수 있다.

```python
numbers = [1, 2, 3, 4, 5, 6, 7]
names = ["철수", "영희", "창수"]
```

<br>

리스트에서 요소의 위치를 인덱스(index)라 하고 인덱스를 통해 요소를 받아 오는 걸 인덱싱(indexing) 이라고 한다.

```python
numbers[0]
names[1]

num_1 = numbers[1]
num_2 = numbers[3]
```

<br>

리스트의 일부를 통째로 자르는 걸 리스트 슬라이싱(list slicing) 이라고 한다.

```python
numbers[0:4]
```

<br>

리스트에 몇 개의 요소가 있는지 확인하는 방법

```python
numbers = []

len(numbers)
```

<br>

리스트 안에 인덱스의 요소를 지우는 방법

```python
numbers = [1, 2, 3, 4, 5]

del numbers[3]
```

<br>

리스트 안에 값을 원하는 위치에 삽입하는 방법

```python
numbers = [1, 2, 3, 4]

# 4번 인덱스에 5를 추가
numbers.insert(4, 5)
```

<br>

리스트의 원소를 모두 출력하는 프로그램

```python
greetings = ["안녕", "니하오", "곤니찌와", "올라", "싸와디캅", "헬로", "봉주르"]

i = 0

while i <= 6:
    print(greetings[i])
```

<br>
온도 단위 바꾸기

```python
# 화씨 온도에서 섭씨 온도로 바꿔 주는 함수
def fahrenheit_to_celsius(fahrenheit):

    return (fahrenheit - 32) * 5 / 9

temperature_list = [40, 15, 32, 64, -4, 11]

print("화씨 온도 리스트: {}".format(temperature_list))  # 화씨 온도 출력

# 리스트의 값들을 화씨에서 섭씨로 변환하는 코드를 입력하세요.
i = 0
while i < len(temperature_list):
    temperature_list[i] = round(fahrenheit_to_celsius(temperature_list[i]), 1)
    i += 1

print("섭씨 온도 리스트: {}".format(temperature_list))  # 섭씨 온도 출력
```

<br>

환전 서비스

```python
# 원화(￦)에서 달러($)로 변환하는 함수
def krw_to_usd(krw):

    return krw / 1000

# 달러($)에서 엔화(￥)로 변환하는 함수
def usd_to_jpy(usd):

    return usd / 8 * 1000

# 원화(￦)으로 각각 얼마인가요?
prices = [34000, 13000, 5000, 21000, 1000, 2000, 8000, 3000]
print("한국 화폐: " + str(prices))

# prices를 원화(￦)에서 달러($)로 변환하기

i = 0
while i < len(prices):
    prices[i] = krw_to_usd(prices[i])
    i += 1

# 달러($)로 각각 얼마인가요?
print("미국 화폐: " + str(prices))

# prices를 달러($)에서 엔화(￥)으로 변환하기

i = 0
while i < len(prices):
    prices[i] = usd_to_jpy(prices[i])
    i += 1

# 엔화(￥)으로 각각 얼마인가요?
print("일본 화폐: " + str(prices))
```

<br>

리스트에서 값의 존재 확인하기

```python
# value가 some_list의 요소인지 확인
def in_list(some_list, value):
    i = 0
    while i < len(some_list):
        # some_list에서 value를 찾으면 True를 리턴
        if some_list[i] == value:
            return True
        i = i + 1

    # 만약 some_list에서 value를 발견하지 못했으면 False를 리턴
    return False

# 테스트
primes = [2, 3, 5, 7, 11, 13, 17, 19, 23]
print(in_list(primes, 7))
print(in_list(primes, 12))

# 또는

primes = [2, 3, 5, 7, 11, 13, 17, 19, 23]
print(7 in primes)
print(12 in primes)

# 거꾸로 값이 없는지 확인하려면 in 앞에 not을 붙이면 된다.

primes = [2, 3, 5, 7, 11, 13, 17, 19, 23]
print(7 not in primes)
print(12 not in primes)
```

<br>

리스트 안의 리스트 (Nested List)

```python
# 세 번의 시험을 보는 수업
grades = [[62, 75, 77], [78, 81, 86], [85, 91, 89]]

# 첫 번째 학생의 성적
print(grades[0])

# 세 번째 학생의 성적
print(grades[2])

# 첫 번째 학생의 첫 번째 시험 성적
print(grades[0][0])

# 세 번째 학생의 두 번째 시험 성적
print(grades[2][1])

# 첫 번째 시험의 평균
print((grades[0][0] + grades[1][0] + grades[2][0]) / 3)

[62, 75, 77]
[85, 91, 89]
62
91
75.0

```

<br>

sort 메소드

새로운 리스트를 생성하지 않고 정렬된 상태로 바꿔준다.

```python
numbers = [5, 3, 7, 1]
numbers.sort()
print(numbers)

[1, 3, 5, 7]
```

<br>

reverse 메소드

원소들을 뒤집어진 순서로 배치한다.

```python
numbers = [5, 3, 7, 1]
numbers.reverse()
print(numbers)

[1, 7, 3, 5]
```

<br>

index 메소드

작성한 값을 갖고 있는 원소의 인덱스를 리턴해준다.

```python
members = ["영훈", "철수", "영희", "혜린"]
print(members.index("철수"))
print(members.index("영희"))

1
2
```

<br>

remove 메소드

첫 번째로 작성한 값을 갖고 있는 원소를 삭제해준다.

```python
fruits = ["딸기", "당근", "파인애플", "수박", "참외", "메론"]
fruits.remove("파인애플")
print(fruits)

['딸기', '당근', '수박', '참외', '메론']
```
