# 1. 단어장

콘솔로 영어 단어와 한국어 뜻을 받고, vocabulary.txt 파일에 단어와 뜻을 정리 <br>
사용자는 반복적으로 단어와 뜻을 입력하는데, 단어나 뜻으로 q를 입력하는 순간 프로그램은 즉시 종료

<br>

```python
with open('vocabulary.txt', 'w') as f:
    while True:
        english_word = input("영어 단어를 입력하세요: ")
        if english_word == 'q':
            break

        korean_word = input("한국어 뜻을 입력하세요: ")
        if korean_word == 'q':
            break

        f.write("{}: {}\n".format(english_word, korean_word))
```

<br>

## 단어 퀴즈

vocabulary.txt를 통해 문제를 내 주는 프로그램 <br>
프로그램은 콘솔에 한국어 뜻을 알려 줄 것이고, 사용자는 그에 맞는 영어 단어를 입력해야 합니다. 사용자가 입력한 영어 단어가 정답이면 "맞았습니다!"라고 출력하고, 틀리면 "아쉽습니다. 정답은 OOO입니다."가 출력

<br>

```python
with open('vocabulary.txt', 'r') as f:
    for line in f:
        data = line.strip().split(": ")
        english_word, korean_word = data[0], data[1]

        # 유저 입력값 받기
        guess = input("{}: ".format(korean_word))

        # 정답 확인하기
        if guess == english_word:
            print("맞았습니다!\n")
        else:
            print("아쉽습니다. 정답은 {}입니다.\n".format(english_word))
```

<br>

## 고급 단어장

random 모듈과 사전(dictionary)을 이용해서 vocabulary.txt의 단어들을 랜덤한 순서로 내도록 프로그램 <br>
같은 단어를 여러번 물어봐도 괜찮고, 프로그램은 사용자가 알파벳 q를 입력할 때까지 계속 실행

<br>

```python
import random

# 사전 만들기
vocab = {}
with open('vocabulary.txt', 'r') as f:
    for line in f:
        data = line.strip().split(": ")
        english_word, korean_word = data[0], data[1]
        vocab[english_word] = korean_word

# 목록 가져오기
keys = list(vocab.keys())

# 문제 내기
while True:
    # 랜덤한 문제 받아오기
    index = random.randint(0, len(keys) - 1)
    english_word = keys[index]
    korean_word = vocab[english_word]

    # 유저 입력값 받기
    guess = input("{}: ".format(korean_word))

    # 프로그램 끝내기
    if guess == 'q':
        break

    # 정답 확인하기
    if guess == english_word:
        print("정답입니다!\n")
    else:
        print("아쉽습니다. 정답은 {}입니다.\n".format(english_word))
```
