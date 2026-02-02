Here are Markdown files for each “Backtracking” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Subsets.md

**Subsets**

**Description:**  
Given an integer array nums, return all possible subsets (the power set).

```python
def subsets(nums):
    res = []
    def backtrack(start, path):
        res.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return res
```

---

### 2. Combination Sum.md

**Combination Sum**

**Description:**  
Given an array of distinct integers candidates and a target integer target, return all unique combinations of candidates where the chosen numbers sum to target.

```python
def combinationSum(candidates, target):
    res = []
    def backtrack(start, path, total):
        if total == target:
            res.append(path[:])
            return
        if total > target:
            return
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            backtrack(i, path, total + candidates[i])
            path.pop()
    backtrack(0, [], 0)
    return res
```

---

### 3. Permutations.md

**Permutations**

**Description:**  
Given an array nums of distinct integers, return all the possible permutations.

```python
def permute(nums):
    res = []
    def backtrack(path, used):
        if len(path) == len(nums):
            res.append(path[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            used[i] = True
            path.append(nums[i])
            backtrack(path, used)
            path.pop()
            used[i] = False
    backtrack([], [False]*len(nums))
    return res
```

---

### 4. Subsets II.md

**Subsets II**

**Description:**  
Given an integer array nums that may contain duplicates, return all possible subsets (the power set) without duplicate subsets.

```python
def subsetsWithDup(nums):
    res = []
    nums.sort()
    def backtrack(start, path):
        res.append(path[:])
        for i in range(start, len(nums)):
            if i > start and nums[i] == nums[i-1]:
                continue
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return res
```

---

### 5. Word Search.md

**Word Search**

**Description:**  
Given an m x n grid of characters and a word, return true if the word exists in the grid.

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])
    path = set()
    def dfs(r, c, i):
        if i == len(word):
            return True
        if (r < 0 or c < 0 or r >= rows or c >= cols or
            word[i] != board[r][c] or (r, c) in path):
            return False
        path.add((r, c))
        res = (dfs(r+1, c, i+1) or dfs(r-1, c, i+1) or
               dfs(r, c+1, i+1) or dfs(r, c-1, i+1))
        path.remove((r, c))
        return res
    for r in range(rows):
        for c in range(cols):
            if dfs(r, c, 0):
                return True
    return False
```

---

### 6. Palindrome Partitioning.md

**Palindrome Partitioning**

**Description:**  
Given a string s, partition s such that every substring of the partition is a palindrome.

```python
def partition(s):
    res = []
    def backtrack(start, path):
        if start == len(s):
            res.append(path[:])
            return
        for end in range(start+1, len(s)+1):
            if s[start:end] == s[start:end][::-1]:
                path.append(s[start:end])
                backtrack(end, path)
                path.pop()
    backtrack(0, [])
    return res
```

---

### 7. Letter Combinations of a Phone Number.md

**Letter Combinations of a Phone Number**

**Description:**  
Given a string containing digits from 2-9, return all possible letter combinations that the number could represent.

```python
def letterCombinations(digits):
    if not digits:
        return []
    phone = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
             '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}
    res = []
    def backtrack(i, path):
        if i == len(digits):
            res.append(''.join(path))
            return
        for c in phone[digits[i]]:
            path.append(c)
            backtrack(i+1, path)
            path.pop()
    backtrack(0, [])
    return res
```

---

### 8. N-Queens.md

**N-Queens**

**Description:**  
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

```python
def solveNQueens(n):
    res = []
    board = [["."]*n for _ in range(n)]
    cols = set()
    pos_diag = set()
    neg_diag = set()
    def backtrack(r):
        if r == n:
            res.append(["".join(row) for row in board])
            return
        for c in range(n):
            if c in cols or (r+c) in pos_diag or (r-c) in neg_diag:
                continue
            cols.add(c)
            pos_diag.add(r+c)
            neg_diag.add(r-c)
            board[r][c] = "Q"
            backtrack(r+1)
            cols.remove(c)
            pos_diag.remove(r+c)
            neg_diag.remove(r-c)
            board[r][c] = "."
    backtrack(0)
    return res
```

---

### 9. Combinations.md

**Combinations**

**Description:**  
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

```python
def combine(n, k):
    res = []
    def backtrack(start, path):
        if len(path) == k:
            res.append(path[:])
            return
        for i in range(start, n+1):
            path.append(i)
            backtrack(i+1, path)
            path.pop()
    backtrack(1, [])
    return res
```

---

### 10. Combination Sum II.md

**Combination Sum II**

**Description:**  
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target. Each number in candidates may only be used once.

```python
def combinationSum2(candidates, target):
    res = []
    candidates.sort()
    def backtrack(start, path, total):
        if total == target:
            res.append(path[:])
            return
        if total > target:
            return
        for i in range(start, len(candidates)):
            if i > start and candidates[i] == candidates[i-1]:
                continue
            path.append(candidates[i])
            backtrack(i+1, path, total + candidates[i])
            path.pop()
    backtrack(0, [], 0)
    return res
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 2 license types
