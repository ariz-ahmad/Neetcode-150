Here are Markdown files for each “Math & Geometry” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Rotate Image.md

**Rotate Image**

**Description:**  
You are given an n x n 2D matrix representing an image. Rotate the image by 90 degrees (clockwise) in-place.

```python
def rotate(matrix):
    matrix.reverse()
    for i in range(len(matrix)):
        for j in range(i):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
```

---

### 2. Spiral Matrix.md

**Spiral Matrix**

**Description:**  
Given an m x n matrix, return all elements of the matrix in spiral order.

```python
def spiralOrder(matrix):
    res = []
    while matrix:
        res += matrix.pop(0)
        if matrix and matrix[0]:
            for row in matrix:
                res.append(row.pop())
        if matrix:
            res += matrix.pop()[::-1]
        if matrix and matrix[0]:
            for row in matrix[::-1]:
                res.append(row.pop(0))
    return res
```

---

### 3. Set Matrix Zeroes.md

**Set Matrix Zeroes**

**Description:**  
Given an m x n integer matrix, if an element is 0, set its entire row and column to 0. Do it in-place.

```python
def setZeroes(matrix):
    rows, cols = len(matrix), len(matrix[0])
    row_zero = False
    for r in range(rows):
        for c in range(cols):
            if matrix[r][c] == 0:
                matrix[0][c] = 0
                if r > 0:
                    matrix[r][0] = 0
                else:
                    row_zero = True
    for r in range(1, rows):
        for c in range(1, cols):
            if matrix[0][c] == 0 or matrix[r][0] == 0:
                matrix[r][c] = 0
    if matrix[0][0] == 0:
        for r in range(rows):
            matrix[r][0] = 0
    if row_zero:
        for c in range(cols):
            matrix[0][c] = 0
```

---

### 4. Valid Sudoku.md

**Valid Sudoku**

**Description:**  
Check if a 9x9 Sudoku board is valid.

```python
def isValidSudoku(board):
    rows = [set() for _ in range(9)]
    cols = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]
    for r in range(9):
        for c in range(9):
            val = board[r][c]
            if val == '.':
                continue
            if val in rows[r] or val in cols[c] or val in boxes[(r//3)*3 + c//3]:
                return False
            rows[r].add(val)
            cols[c].add(val)
            boxes[(r//3)*3 + c//3].add(val)
    return True
```

---

### 5. Pow(x, n).md

**Pow(x, n)**

**Description:**  
Implement pow(x, n), which calculates x raised to the power n.

```python
def myPow(x, n):
    if n == 0:
        return 1
    if n < 0:
        x = 1 / x
        n = -n
    res = 1
    while n:
        if n % 2:
            res *= x
        x *= x
        n //= 2
    return res
```

---

### 6. Multiply Strings.md

**Multiply Strings**

**Description:**  
Given two non-negative integers num1 and num2 represented as strings, return their product as a string.

```python
def multiply(num1, num2):
    if num1 == "0" or num2 == "0":
        return "0"
    res = [0] * (len(num1) + len(num2))
    num1, num2 = num1[::-1], num2[::-1]
    for i in range(len(num1)):
        for j in range(len(num2)):
            res[i + j] += int(num1[i]) * int(num2[j])
            res[i + j + 1] += res[i + j] // 10
            res[i + j] %= 10
    while res[-1] == 0:
        res.pop()
    return ''.join(map(str, res[::-1]))
```

---

### 7. Detect Squares.md

**Detect Squares**

**Description:**  
Design a data structure that can add points and count the number of ways to form axis-aligned squares with those points.

```python
from collections import defaultdict

class DetectSquares:
    def __init__(self):
        self.points = defaultdict(int)

    def add(self, point):
        self.points[tuple(point)] += 1

    def count(self, point):
        res = 0
        px, py = point
        for (x, y), cnt in self.points.items():
            if abs(px - x) == 0 or abs(px - x) != abs(py - y):
                continue
            res += cnt * self.points[(x, py)] * self.points[(px, y)]
        return res
```

---

### 8. Randomized Set.md

**Randomized Set**

**Description:**  
Design a data structure that supports insert, remove, and getRandom in average O(1) time.

```python
import random

class RandomizedSet:
    def __init__(self):
        self.vals = []
        self.idx = {}

    def insert(self, val):
        if val in self.idx:
            return False
        self.idx[val] = len(self.vals)
        self.vals.append(val)
        return True

    def remove(self, val):
        if val not in self.idx:
            return False
        last, i = self.vals[-1], self.idx[val]
        self.vals[i] = last
        self.idx[last] = i
        self.vals.pop()
        del self.idx[val]
        return True

    def getRandom(self):
        return random.choice(self.vals)
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
