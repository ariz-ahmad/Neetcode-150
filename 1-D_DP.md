Here are Markdown files for each “1-D Dynamic Programming” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Climbing Stairs.md

**Climbing Stairs**

**Description:**  
You are climbing a staircase. Each time you can climb 1 or 2 steps. Return the number of distinct ways to reach the top.

```python
def climbStairs(n):
    if n <= 2:
        return n
    a, b = 1, 2
    for _ in range(3, n+1):
        a, b = b, a + b
    return b
```

---

### 2. Min Cost Climbing Stairs.md

**Min Cost Climbing Stairs**

**Description:**  
Given an array cost where cost[i] is the cost of step i, return the minimum cost to reach the top.

```python
def minCostClimbingStairs(cost):
    a, b = 0, 0
    for i in range(2, len(cost)+1):
        a, b = b, min(b + cost[i-1], a + cost[i-2])
    return b
```

---

### 3. House Robber.md

**House Robber**

**Description:**  
Given an array of non-negative integers representing the amount of money of each house, return the maximum amount you can rob without robbing adjacent houses.

```python
def rob(nums):
    rob1, rob2 = 0, 0
    for n in nums:
        rob1, rob2 = rob2, max(rob2, rob1 + n)
    return rob2
```

---

### 4. House Robber II.md

**House Robber II**

**Description:**  
Houses are arranged in a circle. Return the maximum amount you can rob without robbing adjacent houses.

```python
def rob(nums):
    if len(nums) == 1:
        return nums[0]
    def helper(nums):
        rob1, rob2 = 0, 0
        for n in nums:
            rob1, rob2 = rob2, max(rob2, rob1 + n)
        return rob2
    return max(helper(nums[1:]), helper(nums[:-1]))
```

---

### 5. Longest Palindromic Substring.md

**Longest Palindromic Substring**

**Description:**  
Given a string s, return the longest palindromic substring in s.

```python
def longestPalindrome(s):
    res = ""
    for i in range(len(s)):
        # Odd length
        l, r = i, i
        while l >= 0 and r < len(s) and s[l] == s[r]:
            if (r - l + 1) > len(res):
                res = s[l:r+1]
            l -= 1
            r += 1
        # Even length
        l, r = i, i+1
        while l >= 0 and r < len(s) and s[l] == s[r]:
            if (r - l + 1) > len(res):
                res = s[l:r+1]
            l -= 1
            r += 1
    return res
```

---

### 6. Palindromic Substrings.md

**Palindromic Substrings**

**Description:**  
Given a string s, return the number of palindromic substrings in it.

```python
```python
```python
```python
```python
```python
```python
def countSubstrings(s):
    res = 0
    for i in range(len(s)):
        # Odd length
        l, r = i, i
        while l >= 0 and r < len(s) and s[l] == s[r]:
            res += 1
            l -= 1
            r += 1
        # Even length
        l, r = i, i+1
        while l >= 0 and r < len(s) and s[l] == s[r]:
            res += 1
            l -= 1
            r += 1
    return res
```

---

### 7. Decode Ways.md

**Decode Ways**

**Description:**  
Given a string containing only digits, return the number of ways to decode it.

```python
def numDecodings(s):
    if not s:
        return 0
    dp = [0] * (len(s)+1)
    dp[0] = 1
    dp[1] = 0 if s[0] == '0' else 1
    for i in range(2, len(s)+1):
        if s[i-1] != '0':
            dp[i] += dp[i-1]
        if 10 <= int(s[i-2:i]) <= 26:
            dp[i] += dp[i-2]
    return dp[-1]
```

---

### 8. Coin Change.md

**Coin Change**

**Description:**  
Given coins of different denominations and a total amount, return the fewest number of coins needed to make up that amount.

```python
def coinChange(coins, amount):
    dp = [amount+1] * (amount+1)
    dp[0] = 0
    for a in range(1, amount+1):
        for c in coins:
            if a - c >= 0:
                dp[a] = min(dp[a], 1 + dp[a-c])
    return dp[amount] if dp[amount] != amount+1 else -1
```

---

### 9. Maximum Product Subarray.md

**Maximum Product Subarray**

**Description:**  
Given an integer array nums, find the contiguous subarray within an array which has the largest product.

```python
def maxProduct(nums):
    res = max(nums)
    cur_min, cur_max = 1, 1
    for n in nums:
        tmp = cur_max * n
        cur_max = max(n * cur_max, n * cur_min, n)
        cur_min = min(tmp, n * cur_min, n)
        res = max(res, cur_max)
    return res
```

---

### 10. Maximum Subarray.md

**Maximum Subarray**

**Description:**  
Find the contiguous subarray with the largest sum.

```python
def maxSubArray(nums):
    max_sum = nums[0]
    curr = 0
    for n in nums:
        curr = max(n, curr + n)
        max_sum = max(max_sum, curr)
    return max_sum
```

---

### 11. Jump Game.md

**Jump Game**

**Description:**  
Given an array of non-negative integers, return true if you can reach the last index.

```python
def canJump(nums):
    goal = len(nums) - 1
    for i in range(len(nums)-2, -1, -1):
        if i + nums[i] >= goal:
            goal = i
    return goal == 0
```

---

### 12. Jump Game II.md

**Jump Game II**

**Description:**  
Given an array of non-negative integers, return the minimum number of jumps to reach the last index.

```python
def jump(nums):
    res = 0
    l = r = 0
    while r < len(nums) - 1:
        farthest = 0
        for i in range(l, r+1):
            farthest = max(farthest, i + nums[i])
        l = r + 1
        r = farthest
        res += 1
    return res
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 2 license types
