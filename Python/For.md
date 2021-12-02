# 1. for 반복문

```python
my_list = [1, 3, 5, 7, 9]

for number in my_list:
    print(number)

1
3
5
7
9
```

<br>

### range 함수

<br>

```python
for i in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    print(i)

# range 함수

# 파라미터 1개 버전
for i in range(stop):
    print(i)
# 0부터 stop - 1 까지의 범위

# ex)
for i in range(10):
    print(i)

# 파라미터 2개 버전
for i in range(start, stop):
    print(i)
# start부터 stop - 1 까지의 범위

# ex)
for i in range(3, 11):
    print(i)

# 파라미터 3개 버전
for i in range(start, stop, step):
    print(i)
# start부터 stop - 1 까지의 범위, 간격 step

# ex)
for i in range(3, 17, 3):
    print(i)
```

<br>

**range 함수의 장점**

- 간편함
- 깔끔함
- 메모리 효율성

<br>

**거듭제곱**

```python
for i in range(11):
    print('{}^{} = {}'.format(2, i, 2 ** i))
```

<br>

**for 문으로 구구단**

```python
for i in range(1, 10):
    for j in range(1, 10):
        print('{} * {} = {}'.format(i, j, i*j))
```

<br>

**피타고라스 삼조**

```python
for a in range(1, 400):
    for b in range(1, 400):
        c = 400 - a - b
        if a * a + b * b == c * c and a < b < c:
            print(a * b * c)
```

<br>

**리스트 뒤집기**

```python
numbers = [2, 3, 5, 7, 11, 13, 17, 19]

# 리스트 뒤집기
for left in range(len(numbers) // 2):
    # 인덱스 left와 대칭인 인덱스 right 계산
    right = len(numbers) - left - 1

    # 위치 바꾸기
    numbers[right], numbers[left] = numbers[left], numbers[right]

print("뒤집어진 리스트: " + str(numbers))
```
