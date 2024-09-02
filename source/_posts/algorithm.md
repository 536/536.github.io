---
title: Algorithm
date: 2024-09-03 00:35:11
tags:
    - algorithm
---

## 求最大公约数

```python
x, y = a, b = [int(i) for i in input().split()]
# 辗转相除法求最大公约数
while y:
    x, y = y, x % y
print(x)
```

## 求最小公倍数

```python
x, y = a, b = [int(i) for i in input().split()]
# 辗转相除法求最大公约数
while y:
    x, y = y, x % y
# 最小公倍数为两数之积除以最大公约数
print(int(a * b / x))
```

## 求解立方根

```python
x = float(input())
sign: int = [-1, 1][x > 0]
x = abs(x)
# solution 1 - built-in algorithm
# print(round(x ** (1 / 3), 1) * sign)

# solution 2 - binary search
m, n = min(1.0, x), max(1.0, x)
while True:
    mid = (m + n) / 2
    if abs(mid ** 3 - x) <= 0.1 ** 3:
        print(round(m, 1) * sign)
        break
    if mid ** 3 > x:
        m, n = m, (m + n) / 2
    else:
        m, n = (m + n) / 2, n
```

## 八皇后问题

```python
from dataclasses import dataclass
from typing import Any, Generator, Iterator, List

@dataclass
class Point:
    x: int
    y: int
    def bearable(self, p1: "Point") -> bool:
        if self.x == p1.x or self.y == p1.y:
            return False
        if abs(self.y - p1.y) == abs(self.x - p1.x):
            return False
        return True

def row_points(row_num: int) -> Generator[Point, Any, None]:
    return (Point(row_num, col_num) for col_num in range(8))

def bearable_points(current: List[Point], points: Iterator[Point]):
    return (point for point in points if all(p.bearable(point) for p in current))

def queen(solution=None, row_num=0):
    solution = solution or []
    if len(solution) == 8:
        print([point.y for point in solution])
    for point in bearable_points(solution, row_points(row_num)):
        queen([*solution, point], row_num + 1)

queen()
```
