---
title: 八皇后问题
date: 2024-03-09 23:37:07
tags:
    - algorithm
---

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
