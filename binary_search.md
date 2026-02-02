Here are Markdown files for each “Binary Search” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Binary Search.md

**Binary Search**

**Description:**  
Given a sorted array and a target value, return the index if the target is found. If not, return -1.

```python
def search(nums, target):
    l, r = 0, len(nums) - 1
    while l <= r:
        m = (l + r) // 2
        if nums[m] == target:
            return m
        elif nums[m] < target:
            l = m + 1
        else:
            r = m - 1
    return -1
```

---

### 2. Search a 2D Matrix.md

**Search a 2D Matrix**

**Description:**  
Write an efficient algorithm that searches for a value in an m x n matrix. Integers in each row are sorted from left to right, and the first integer of each row is greater than the last integer of the previous row.

```python
def searchMatrix(matrix, target):
    if not matrix or not matrix[0]:
        return False
    rows, cols = len(matrix), len(matrix[0])
    l, r = 0, rows * cols - 1
    while l <= r:
        m = (l + r) // 2
        val = matrix[m // cols][m % cols]
        if val == target:
            return True
        elif val < target:
            l = m + 1
        else:
            r = m - 1
    return False
```

---

### 3. Koko Eating Bananas.md

**Koko Eating Bananas**

**Description:**  
Given piles of bananas and an integer h, return the minimum integer k such that Koko can eat all the bananas within h hours.

```python
def minEatingSpeed(piles, h):
    l, r = 1, max(piles)
    while l < r:
        k = (l + r) // 2
        hours = sum((pile + k - 1) // k for pile in piles)
        if hours > h:
            l = k + 1
        else:
            r = k
    return l
```

---

### 4. Find Minimum in Rotated Sorted Array.md

**Find Minimum in Rotated Sorted Array**

**Description:**  
Suppose an array sorted in ascending order is rotated at some pivot. Find the minimum element.

```python
def findMin(nums):
    l, r = 0, len(nums) - 1
    while l < r:
        m = (l + r) // 2
        if nums[m] > nums[r]:
            l = m + 1
        else:
            r = m
    return nums[l]
```

---

### 5. Search in Rotated Sorted Array.md

**Search in Rotated Sorted Array**

**Description:**  
Given a rotated sorted array and a target value, return its index. If not found, return -1.

```python
def search(nums, target):
    l, r = 0, len(nums) - 1
    while l <= r:
        m = (l + r) // 2
        if nums[m] == target:
            return m
        if nums[l] <= nums[m]:
            if nums[l] <= target < nums[m]:
                r = m - 1
            else:
                l = m + 1
        else:
            if nums[m] < target <= nums[r]:
                l = m + 1
            else:
                r = m - 1
    return -1
```

---

### 6. Time Based Key-Value Store.md

**Time Based Key-Value Store**

**Description:**  
Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key’s value at a certain timestamp.

```python
from collections import defaultdict
import bisect

class TimeMap:
    def __init__(self):
        self.store = defaultdict(list)

    def set(self, key, value, timestamp):
        self.store[key].append((timestamp, value))

    def get(self, key, timestamp):
        arr = self.store[key]
        i = bisect.bisect_right(arr, (timestamp, chr(127)))
        return arr[i-1][1] if i else ""
```

---

### 7. Median of Two Sorted Arrays.md

**Median of Two Sorted Arrays**

**Description:**  
Given two sorted arrays, return the median of the two sorted arrays.

```python
def findMedianSortedArrays(nums1, nums2):
    A, B = nums1, nums2
    total = len(A) + len(B)
    half = total // 2
    if len(B) < len(A):
        A, B = B, A
    l, r = 0, len(A) - 1
    while True:
        i = (l + r) // 2
        j = half - i - 2
        Aleft = A[i] if i >= 0 else float('-inf')
        Aright = A[i+1] if (i+1) < len(A) else float('inf')
        Bleft = B[j] if j >= 0 else float('-inf')
        Bright = B[j+1] if (j+1) < len(B) else float('inf')
        if Aleft <= Bright and Bleft <= Aright:
            if total % 2:
                return min(Aright, Bright)
            return (max(Aleft, Bleft) + min(Aright, Bright)) / 2
        elif Aleft > Bright:
            r = i - 1
        else:
            l = i + 1
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
