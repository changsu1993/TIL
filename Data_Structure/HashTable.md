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
