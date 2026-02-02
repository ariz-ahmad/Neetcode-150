Here are Markdown files for each “2-D Dynamic Programming” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Unique Paths.md

**Unique Paths**

**Description:**  
A robot is located at the top-left corner of an m x n grid. The robot can only move either down or right at any point in time. Return the number of possible unique paths to the bottom-right corner.

```python
def uniquePaths(m, n):
    dp = [[1]*n for _ in range(m)]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    return dp[-1][-1]
```

---

### 2. Longest Common Subsequence.md

**Longest Common Subsequence**

**Description:**  
Given two strings text1 and text2, return the length of their longest common subsequence.

```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0]*(n+1) for _ in range(m+1)]
    for i in range(m-1, -1, -1):
        for j in range(n-1, -1, -1):
            if text1[i] == text2[j]:
                dp[i][j] = 1 + dp[i+1][j+1]
            else:
                dp[i][j] = max(dp[i+1][j], dp[i][j+1])
    return dp[0][0]
```

---

### 3. Coin Change II.md

**Coin Change II**

**Description:**  
You are given coins of different denominations and a total amount. Return the number of combinations that make up that amount.

```python
def change(amount, coins):
    dp = [0] * (amount + 1)
    dp[0] = 1
    for coin in coins:
        for x in range(coin, amount + 1):
            dp[x] += dp[x - coin]
    return dp[amount]
```

---

### 4. Longest Increasing Path in a Matrix.md

**Longest Increasing Path in a Matrix**

**Description:**  
Given an m x n integers matrix, return the length of the longest increasing path in matrix.

```python
def longestIncreasingPath(matrix):
    if not matrix:
        return 0
    m, n = len(matrix), len(matrix[0])
    dp = [[0]*n for _ in range(m)]
    def dfs(i, j):
        if dp[i][j]:
            return dp[i][j]
        val = matrix[i][j]
        res = 1
        for x, y in [(0,1),(1,0),(-1,0),(0,-1)]:
            ni, nj = i + x, j + y
            if 0 <= ni < m and 0 <= nj < n and matrix[ni][nj] > val:
                res = max(res, 1 + dfs(ni, nj))
        dp[i][j] = res
        return res
    return max(dfs(i, j) for i in range(m) for j in range(n))
```

---

### 5. Distinct Subsequences.md

**Distinct Subsequences**

**Description:**  
Given two strings s and t, return the number of distinct subsequences of s which equals t.

```python
def numDistinct(s, t):
    m, n = len(s), len(t)
    dp = [[0]*(n+1) for _ in range(m+1)]
    for i in range(m+1):
        dp[i][n] = 1
    for i in range(m-1, -1, -1):
        for j in range(n-1, -1, -1):
            if s[i] == t[j]:
                dp[i][j] = dp[i+1][j+1] + dp[i+1][j]
            else:
                dp[i][j] = dp[i+1][j]
    return dp[0][0]
```

---

### 6. Interleaving String.md

**Interleaving String**

**Description:**  
Given strings s1, s2, and s3, return true if s3 is formed by an interleaving of s1 and s2.

```python
def isInterleave(s1, s2, s3):
    m, n = len(s1), len(s2)
    if m + n != len(s3):
        return False
    dp = [[False]*(n+1) for _ in range(m+1)]
    dp[0][0] = True
    for i in range(m+1):
        for j in range(n+1):
            if i > 0:
                dp[i][j] |= dp[i-1][j] and s1[i-1] == s3[i+j-1]
            if j > 0:
                dp[i][j] |= dp[i][j-1] and s2[j-1] == s3[i+j-1]
    return dp[m][n]
```

---

### 7. Edit Distance.md

**Edit Distance**

**Description:**  
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

```python
def minDistance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0]*(n+1) for _ in range(m+1)]
    for i in range(m+1):
        dp[i][0] = i
    for j in range(n+1):
        dp[0][j] = j
    for i in range(1, m+1):
        for j in range(1, n+1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
    return dp[m][n]
```

---

### 8. Regular Expression Matching.md

**Regular Expression Matching**

**Description:**  
Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*'.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False]*(n+1) for _ in range(m+1)]
    dp[m][n] = True
    for i in range(m, -1, -1):
        for j in range(n-1, -1, -1):
            first_match = i < m and (s[i] == p[j] or p[j] == '.')
            if j+1 < n and p[j+1] == '*':
                dp[i][j] = dp[i][j+2] or (first_match and dp[i+1][j])
            else:
                dp[i][j] = first_match and dp[i+1][j+1]
    return dp[0][0]
```

---

### 9. Wildcard Matching.md

**Wildcard Matching**

**Description:**  
Given an input string s and a pattern p, implement wildcard pattern matching with support for '?' and '*'.

```python
def isMatch(s, p):
    m, n = len(s), len(p)
    dp = [[False]*(n+1) for _ in range(m+1)]
    dp[m][n] = True
    for i in range(m, -1, -1):
        for j in range(n-1, -1, -1):
            first_match = i < m and (s[i] == p[j] or p[j] == '?')
            if p[j] == '*':
                dp[i][j] = dp[i][j+1] or (i < m and dp[i+1][j])
            else:
                dp[i][j] = first_match and dp[i+1][j+1]
    return dp[0][0]
```

---

### 10. Maximum Profit in Job Scheduling.md

**Maximum Profit in Job Scheduling**

**Description:**  
Given n jobs, return the maximum profit you can take such that no two jobs overlap.

```python
import bisect

def jobScheduling(startTime, endTime, profit):
    jobs = sorted(zip(startTime, endTime, profit), key=lambda x: x[1])
    dp = [(0, 0)]
    for s, e, p in jobs:
        i = bisect.bisect_right(dp, (s, float('inf'))) - 1
        if dp[i][1] + p > dp[-1][1]:
            dp.append((e, dp[i][1] + p))
    return dp[-1][1]
```

---

### 11. Burst Balloons.md

**Burst Balloons**

**Description:**  
Given n balloons, each with a number on it, return the maximum coins you can collect by bursting the balloons wisely.

```python
def maxCoins(nums):
    nums = [1] + nums + [1]
    n = len(nums)
    dp = [[0]*n for _ in range(n)]
    for length in range(2, n):
        for left in range(n - length):
            right = left + length
            for k in range(left+1, right):
                dp[left][right] = max(dp[left][right],
                                      nums[left]*nums[k]*nums[right] + dp[left][k] + dp[k][right])
    return dp[0][n-1]
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 4 license types
