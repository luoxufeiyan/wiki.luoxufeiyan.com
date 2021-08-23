# Python3 小抄速记

## 判断质数
```
def is_prime(n):
    # Only used to test >2 odd numbers.
    return all(n % d for d in range(3, round(sqrt(n)) + 1, 2))
```