# 1. Dictionary

key - value 가 하나의 쌍을 이룬다.

```python
my_dictionary = {
  5: 25,
  2: 4,
  3: 9
}

print(my_dictionary[3]) # 9

my_dictionary[7] = 49

print(my_dictionary) # {5: 25, 2: 4, 3: 9, 7: 49}


word = {
  '가': '가방',
  '나': '나비',
  '다': '다람쥐'
}
```

<br>

### 사전과 리스트의 차이점

- 리스트는 인덱스가 순서대로 진행되지만 사전은 순서라는 개념이 없다.
- 리스트의 인덱스는 무조건 정숫값이지만 사전의 키는 정수형일 필요가 없다.

<br>

**단어장 만들기**

```python
# 1. 단어장 만들기
vocab = {
    'sanitizer': '살균제',
    'ambition': '야망',
    'conscience': '양심',
    'civilization': '문명'
}
print(vocab)
# {'sanitizer': '살균제', 'ambition': '야망', 'conscience': '양심', 'civilization': '문명'}


# 2. 새로운 단어들 추가
vocab['privilege'] = '특권'
vocab['principle'] = '원칙'
print(vocab)
# {'sanitizer': '살균제', 'ambition': '야망', 'conscience': '양심', 'civilization': '문명', 'privilege': '특권', 'principle': '원칙'}

```

<br>

**사전에 어떤 값들이 있는지 목록이 필요할 때 or key를 받아오고 싶을 때**

```python
vocab = {
    'sanitizer': '살균제',
    'ambition': '야망',
    'conscience': '양심',
    'civilization': '문명'
}

print(vocab.values())
# dict_values(['살균제', '야망', '양심', '문명'])

print('문명' in vocab.values())
# True

for value in vocab.values():
    print(value)
# 살균제
# 야망
# 양심
# 문명

print(vocab.keys())
# dict_keys('sanitizer', 'ambition', 'conscience', 'civilization')

for key in vocab.keys():
    print(key)
# sanitizer
# ambition
# conscience
# civilization

for key, value in vocab.items():
    print(key, value)
# sanitizer 살균제
# ambition 야망
# conscience 양심
# civilization 문명
```

<br>

**사전 뒤집기**

```python
# 언어 사전의 단어와 뜻을 서로 바꿔주는 함수
def reverse_dict(dict):
    new_dict = {}  # 새로운 사전

    # dict의 key와 value를 뒤집어서 new_dict에 저장
    for key, value in dict.items():
        new_dict[value] = key


    return new_dict  # 변환한 새로운 사전 리턴


# 영-한 단어장
vocab = {
    'sanitizer': '살균제',
    'ambition': '야망',
    'conscience': '양심',
    'civilization': '문명',
    'privilege': '특권',
    'principles': '원칙'
}

# 기존 단어장 출력
print("영-한 단어장\n{}\n".format(vocab))

# 영-한 단어장
# {'sanitizer': '살균제', 'ambition': '야망', 'conscience': '양심', 'civilization': '문명', 'privilege': '특권', 'principles': '원칙'}

# 변환된 단어장 출력
reversed_vocab = reverse_dict(vocab)
print("한-영 단어장\n{}".format(reversed_vocab))

# 한-영 단어장
# {'살균제': 'sanitizer', '야망': 'ambition', '양심': 'conscience', '문명': 'civilization', '특권': 'privilege', '원칙': 'principles'}
```

<br>

**투표 집계하기**

```python
# 투표 결과 리스트
votes = ['김영자', '강승기', '최만수', '김영자', '강승기', '강승기', '최만수', '김영자', \
'최만수', '김영자', '최만수', '김영자', '김영자', '최만수', '최만수', '최만수', '강승기', \
'강승기', '김영자', '김영자', '최만수', '김영자', '김영자', '강승기', '김영자']

# 후보별 득표수 사전
vote_counter = {}

# 리스트 votes를 이용해서 사전 vote_counter를 정리하기
for name in votes:
    if name not in vote_counter:
        vote_counter[name] = 1
    else:
        vote_counter[name] += 1

# 후보별 득표수 출력
print(vote_counter)

# {'김영자': 11, '강승기': 6, '최만수': 8}
```
