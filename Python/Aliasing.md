# 1. Aliasing

파이썬에서 두 변수가 가리키는 메모리 주소가 같으면 서로의 alias 라고 한다. <br>
문자열처럼 그 자체의 값이 변경 불가능한 값은 alias를 생성해도 안전하지만, <br>
리스트 같은 가변적인 값은 alias를 생성하게 되면 프로그램의 흐름이 개발자의 의도와 다르게 흘러갈 수 있다.

<br>

```python
x = 5
y = x
y = 3
print(x) # 5
print(y) # 3

x = [2, 3, 5, 7, 11]
y = x
y[2] = 4
print(x) # [2, 3, 4, 7, 11]
print(y) # [2, 3, 4, 7, 11]
# y는 x의 가명 또는 alias라고 할 수 있다.

# y를 바꾸면서 x의 값은 그대로 유지하려면

x = [2, 3, 5, 7, 11]
y = list(x)
y[2] = 4
print(x) # [2, 3, 5, 7, 11]
print(y) # [2, 3, 4, 7, 11]
```

<br>

**리스트와 문자열**

리스트는 문자열과 굉장히 유사한 구조를 지니고 있다. <br>
리스트는 어떤 자료형을 나열한 거라면 문자열은 문자를 나열한 거라고 볼 수 있다. <br>

<br>

```python
alphabet_list[] = ['A', 'B', 'C', 'D', 'E']

print(alphabet_list[0]) # A
print(alphabet_list[1]) # B
print(alphabet_list[2]) # C

print(alphabet_list[0:3]) # ['A', 'B', 'C']

list_1 = [1, 2, 3]
list_2 = [4, 5, 6]
list_3 = list_1 + list_2
print(list_3) # [1, 2, 3, 4, 5, 6]

my_list = [1, 2, 3, 4, 5]
print(len(my_list)) # 5

# 알파벳 리스트의 반복문
alphabets_list = ['H', 'E', 'L', 'L', 'O']
for alphabet in alphabets_list:
    print(alphabet)

print(alphabet_string[0]) # A
print(alphabet_string[1]) # B
print(alphabet_string[2]) # C

print(alphabet_string[0:3]) # ABC

str_1 = 'Hello'
str_2 = 'World'
str_3 = str_1 + str_2
print(str_3) # HelloWorld

my_string = 'Hello World'
print(len(my_string)) # 11

# 알파벳 문자열의 반복문
alphabets_string = 'HELLO'
for alphabet in alphabets_string:
    print(alphabet)

# --- 차이점 ---

numbers = [1, 2, 3, 4]
numbers[0] = 5
print(numbers) # [5, 2, 3, 4]

name = 'Hello'
name[0] = 'A'
print(name) # Error : 리스트와 달리 문자열은 수정이 불가능
```

<br>

**자릿수 합 구하기**

```python
# 자리수 합 리턴
def sum_digit(num):
    total = 0
    str_num = str(num)

    for i in str_num:
        total += int(i)

    return total

# sum_digit(1)부터 sum_digit(1000)까지의 합 구하기
digit_total = 0
for i in range(1, 1001):
    digit_total += sum_digit(i)

print(digit_total) # 13501
```

<br>

**주민등록번호 가리기**

```python
# 접근법 #1
"""
문자열을 리스트로 변환한 후, 마지막 네 원소를 '*'로 수정한다.
그리고 다시 리스트를 하나의 문자열로 합친다.
"""

def mask_security_number(security_number):
    i = 1
    removed_list = list(security_number)

    while i < 5 :
        removed_list[-i] = "*"
        i += 1

    removed_str = "".join(removed_list)

    return removed_str

# or

def mask_security_number(security_number):
    num_list = list(security_number)

    # 마지막 네 값을 *로 대체
    for i in range(len(num_list) - 4, len(num_list)):
        num_list[i] = '*'

    # 리스트를 문자열로 복구하여 반환
    return ''.join(num_list)

# 접근법 #1-1
"""
접근법 #1 과 접근법은 똑같지만 다른 코드
"""

def mask_security_number(security_number):
    # security_number를 리스트로 변환
    num_list = list(security_number)

    # 마지막 네 값을 *로 대체
    for i in range(len(num_list) - 4, len(num_list)):
        num_list[i] = "*"

    # 리스트를 문자열로 복구
    total_str = ""
    for i in range(len(num_list)):
        total_str += num_list[i]

    return total_str

# 접근법 #2
"""
문자열 슬라이싱을 이용
"""

def mask_security_number(security_number):
    return security_number[:-4] + '****'


# 테스트
print(mask_security_number("880720-1234567"))  # 880720-123****
print(mask_security_number("8807201234567"))  # 880720123****
print(mask_security_number("930124-7654321"))  # 930124-765****
print(mask_security_number("9301247654321"))  # 930124765****
print(mask_security_number("761214-2357111"))  # 761214-235****
print(mask_security_number("7612142357111"))  # 761214235****
```

<br>

**팰린드롬**

```python
# 접근법 #1
def is_palindrome(word):
    if word == word[::-1]:
        return True
    else:
        return False

# 접근법 #2
def is_palindrome(word):
    for left in range(len(word) // 2):
        # 한 쌍이라도 일치하지 않으면 바로 False를 리턴하고 함수를 끝냄
        right = len(word) - left - 1
        if word[left] != word[right]:
            return False

    # for문에서 나왔다면 모든 쌍이 일치
    return True

# 테스트
print(is_palindrome("racecar"))
print(is_palindrome("stars"))
print(is_palindrome("토마토"))
print(is_palindrome("kayak"))
print(is_palindrome("hello"))
```
