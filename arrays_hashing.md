I will generate Markdown files for each “Arrays & Hashing” problem from NeetCode 150 in Python, with a brief description and a full solution. You can then save these as individual `.md` files.

---

### 1. Contains Duplicate.md

**Contains Duplicate**

**Description:**  
Check if any value appears at least twice in the array.

```python
def containsDuplicate(nums):
    return len(nums) != len(set(nums))
```

---

### 2. Valid Anagram.md

**Valid Anagram**

**Description:**  
Check if two strings are anagrams of each other.

```python
def isAnagram(s, t):
    return sorted(s) == sorted(t)
```

---

### 3. Two Sum.md

**Two Sum**

**Description:**  
Return indices of the two numbers such that they add up to a specific target.

```python
def twoSum(nums, target):
    lookup = {}
    for i, num in enumerate(nums):
        if target - num in lookup:
            return [lookup[target - num], i]
        lookup[num] = i
```

---

### 4. Group Anagrams.md

**Group Anagrams**

**Description:**  
Group strings that are anagrams of each other.

```python
from collections import defaultdict

def groupAnagrams(strs):
    res = defaultdict(list)
    for s in strs:
        key = tuple(sorted(s))
        res[key].append(s)
    return list(res.values())
```

---

### 5. Top K Frequent Elements.md

**Top K Frequent Elements**

**Description:**  
Return the k most frequent elements in the array.

```python
from collections import Counter

def topKFrequent(nums, k):
    count = Counter(nums)
    return [item for item, _ in count.most_common(k)]
```

---

### 6. Product of Array Except Self.md

**Product of Array Except Self**

**Description:**  
Return an array such that each element is the product of all elements except itself.

```python
def productExceptSelf(nums):
    res = [1] * len(nums)
    left = 1
    for i in range(len(nums)):
        res[i] = left
        left *= nums[i]
    right = 1
    for i in range(len(nums)-1, -1, -1):
        res[i] *= right
        right *= nums[i]
    return res
```

---

### 7. Valid Sudoku.md

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

### 8. Longest Consecutive Sequence.md

**Longest Consecutive Sequence**

**Description:**  
Find the length of the longest consecutive elements sequence.

```python
def longestConsecutive(nums):
    num_set = set(nums)
    longest = 0
    for n in num_set:
        if n - 1 not in num_set:
            length = 1
            while n + length in num_set:
                length += 1
            longest = max(longest, length)
    return longest
```

---

### 9. Encode and Decode Strings.md

**Encode and Decode Strings**

**Description:**  
Design an algorithm to encode a list of strings to a string and decode it back to the list of strings.

```python
def encode(strs):
    return ''.join(f'{len(s)}#{s}' for s in strs)

def decode(s):
    res, i = [], 0
    while i < len(s):
        j = i
        while s[j] != '#':
            j += 1
        length = int(s[i:j])
        res.append(s[j+1:j+1+length])
        i = j + 1 + length
    return res
```

---

You can copy each block above into its own `.md` file, named as shown, for the “Arrays & Hashing” section. Let me know if you want these as a single combined Markdown file or need help with the next topic!
