# 1. 매출 평균

12월 하루 평균 매출을 출력 후 평균을 구하기 위해서 총 매출을 총 일수로 나누기

<br>

```python
with open('data/chicken.txt', 'r') as f:
    total_revenue = 0
    total_days = 0

    for price in f:
        price_space = price.strip().split(": ")
        revenue = int(price_space[1])

        total_revenue += revenue
        total_days += 1

    print(total_revenue / total_days)
```
