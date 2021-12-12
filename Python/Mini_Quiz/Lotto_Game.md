# 1. 로또 게임

로또 시뮬레이션 프로그램 <br>
로또는 주 1회씩 열리고 한 사람이 한 회차에 여러 번 참여 가능 <br>
번호는 1부터 45까지, 주최측에서는 매주 6개의 '일반 당첨 번호'와 1개의 '보너스 번호'를 뽑는다. <br>
참가자는 1번 참여할 때마다 서로 다른 번호 6개를 선택한다. <br>

당첨 액수

1. 내가 뽑은 번호 6개와 일반 당첨 번호 6개 모두 일치 (10억 원)
2. 내가 뽑은 번호 5개와 일반 당첨 번호 5개 일치, 그리고 내 번호 1개와 보너스 번호 일치 (5천만 원)
3. 내가 뽑은 번호 5개와 일반 당첨 번호 5개 일치 (100만 원)
4. 내가 뽑은 번호 4개와 일반 당첨 번호 4개 일치 (5만 원)
5. 내가 뽑은 번호 3개와 일반 당첨 번호 3개 일치 (5천 원)

<br>

```python
from random import randint


def generate_numbers(n):
    numbers = []

    while len(numbers) < n:
        num = randint(1, 45)
        if num not in numbers:
            numbers.append(num)

    return numbers


def draw_winning_numbers():
    winning_numbers = generate_numbers(7)
    return sorted(winning_numbers[:6]) + winning_numbers[6:]


def count_matching_numbers(numbers, winning_numbers):
    count = 0

    for num in numbers:
        if num in winning_numbers:
            count = count + 1

    return count


def check(numbers, winning_numbers):
    count = count_matching_numbers(numbers, winning_numbers[:6])
    bonus_count = count_matching_numbers(numbers, winning_numbers[6:])

    if count == 6:
        return 100000000
    elif count == 5 and bonus_count == 1:
        return 50000000
    elif count == 5:
        return 1000000
    elif count == 4:
        return 50000
    elif count == 3:
        return 5000
    else:
        return 0
```
