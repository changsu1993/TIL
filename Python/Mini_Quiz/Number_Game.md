# 1. 숫자 맞추기 게임

1과 20 사이의 숫자를 맞히는 게임

<br>

```python
import random

NUM_TRIES = 4
ANSWER = random.randint(1, 20)
guess = -1
tries = 0

while guess != ANSWER and tries < NUM_TRIES:
    guess = int(input("기회가 {}번 남았습니다. 1-20 사이의 숫자를 맞혀보세요: ".format(NUM_TRIES - tries)))
    tries += 1

    if ANSWER > guess:
        print("Up")
    elif ANSWER < guess:
        print("Down")

if guess == ANSWER:
    print("축하합니다. {}번 만에 숫자를 맞히셨습니다.".format(tries))
else:
    print("아쉽습니다. 정답은 {}입니다.".format(ANSWER))

if random_score == number:
    print("축하합니다. {}번 만에 숫자를 맞히셨습니다.".format(score))
elif random_score > score:
    if number > random_score:
        print("Down")
    elif number < random_score:
        print("Up")
    input("기회가 {}번 남았습니다. 1-20 사이의 숫자를 맞혀보세요: {}".format(score-1, number)
elif random_score < score:
    print("아쉽습니다. 정답은 {}입니다.".format(random_score))
```
