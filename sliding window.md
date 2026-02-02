Here are Markdown files for each “Sliding Window” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Best Time to Buy and Sell Stock.md

**Best Time to Buy and Sell Stock**

**Description:**  
Given an array where each element is the price of a stock on a given day, find the maximum profit you can achieve by buying and selling once.

```python
def maxProfit(prices):
    min_price = float('inf')
    max_profit = 0
    for price in prices:
        min_price = min(min_price, price)
        max_profit = max(max_profit, price - min_price)
    return max_profit
```

---

### 2. Longest Substring Without Repeating Characters.md

**Longest Substring Without Repeating Characters**

**Description:**  
Given a string, find the length of the longest substring without repeating characters.

```python
def lengthOfLongestSubstring(s):
    char_set = set()
    l = res = 0
    for r in range(len(s)):
        while s[r] in char_set:
            char_set.remove(s[l])
            l += 1
        char_set.add(s[r])
        res = max(res, r - l + 1)
    return res
```

---

### 3. Longest Repeating Character Replacement.md

**Longest Repeating Character Replacement**

**Description:**  
Given a string and an integer k, find the length of the longest substring that can be obtained by replacing at most k characters with any letter so that all the characters in the substring are the same.

```python
def characterReplacement(s, k):
    count = {}
    res = l = 0
    for r in range(len(s)):
        count[s[r]] = 1 + count.get(s[r], 0)
        while (r - l + 1) - max(count.values()) > k:
            count[s[l]] -= 1
            l += 1
        res = max(res, r - l + 1)
    return res
```

---

### 4. Permutation in String.md

**Permutation in String**

**Description:**  
Given two strings s1 and s2, return true if s2 contains a permutation of s1.

```python
def checkInclusion(s1, s2):
    from collections import Counter
    if len(s1) > len(s2):
        return False
    s1_count = Counter(s1)
    window = Counter(s2[:len(s1)])
    if window == s1_count:
        return True
    for i in range(len(s1), len(s2)):
        window[s2[i]] += 1
        window[s2[i - len(s1)]] -= 1
        if window[s2[i - len(s1)]] == 0:
            del window[s2[i - len(s1)]]
        if window == s1_count:
            return True
    return False
```

---

### 5. Minimum Window Substring.md

**Minimum Window Substring**

**Description:**  
Given two strings s and t, return the minimum window in s which will contain all the characters in t.

```python
def minWindow(s, t):
    from collections import Counter
    if not t or not s:
        return ""
    count_t = Counter(t)
    window = {}
    have, need = 0, len(count_t)
    res, res_len = [-1, -1], float('inf')
    l = 0
    for r, c in enumerate(s):
        window[c] = 1 + window.get(c, 0)
        if c in count_t and window[c] == count_t[c]:
            have += 1
        while have == need:
            if (r - l + 1) < res_len:
                res = [l, r]
                res_len = r - l + 1
            window[s[l]] -= 1
            if s[l] in count_t and window[s[l]] < count_t[s[l]]:
                have -= 1
            l += 1
    l, r = res
    return s[l:r+1] if res_len != float('inf') else ""
```

---

### 6. Sliding Window Maximum.md

**Sliding Window Maximum**

**Description:**  
Given an array and an integer k, find the maximum value in each sliding window of size k.

```python
from collections import deque

def maxSlidingWindow(nums, k):
    output = []
    q = deque()
    l = r = 0
    while r < len(nums):
        while q and nums[q[-1]] < nums[r]:
            q.pop()
        q.append(r)
        if l > q[0]:
            q.popleft()
        if (r + 1) >= k:
            output.append(nums[q[0]])
            l += 1
        r += 1
    return output
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
