Here are Markdown files for each “Heap / Priority Queue” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Kth Largest Element in an Array.md

**Kth Largest Element in an Array**

**Description:**  
Find the kth largest element in an unsorted array.

```python
import heapq

def findKthLargest(nums, k):
    return heapq.nlargest(k, nums)[-1]
```

---

### 2. Last Stone Weight.md

**Last Stone Weight**

**Description:**  
You are given a list of stones with positive integer weights. Each turn, smash the two heaviest stones together. Return the weight of the last remaining stone (or 0 if none remain).

```python
import heapq

def lastStoneWeight(stones):
    stones = [-s for s in stones]
    heapq.heapify(stones)
    while len(stones) > 1:
        first = -heapq.heappop(stones)
        second = -heapq.heappop(stones)
        if first != second:
            heapq.heappush(stones, -(first - second))
    return -stones[0] if stones else 0
```

---

### 3. K Closest Points to Origin.md

**K Closest Points to Origin**

**Description:**  
Given an array of points on the X-Y plane, return the k closest points to the origin (0, 0).

```python
import heapq

def kClosest(points, k):
    return heapq.nsmallest(k, points, key=lambda x: x[0]**2 + x[1]**2)
```

---

### 4. Kth Smallest Element in a Sorted Matrix.md

**Kth Smallest Element in a Sorted Matrix**

**Description:**  
Given an n x n matrix where each of the rows and columns is sorted in ascending order, return the kth smallest element in the matrix.

```python
import heapq

def kthSmallest(matrix, k):
    n = len(matrix)
    minHeap = []
    for r in range(min(k, n)):
        heapq.heappush(minHeap, (matrix[r][0], r, 0))
    for _ in range(k):
        val, r, c = heapq.heappop(minHeap)
        if c + 1 < n:
            heapq.heappush(minHeap, (matrix[r][c+1], r, c+1))
    return val
```

---

### 5. Task Scheduler.md

**Task Scheduler**

**Description:**  
Given a list of tasks and a cooldown interval n, return the least number of units of times that the CPU will take to finish all the given tasks.

```python
from collections import Counter

def leastInterval(tasks, n):
    count = Counter(tasks)
    max_freq = max(count.values())
    max_count = list(count.values()).count(max_freq)
    return max(len(tasks), (max_freq - 1) * (n + 1) + max_count)
```

---

### 6. Find Median from Data Stream.md

**Find Median from Data Stream**

**Description:**  
Design a data structure that supports adding numbers and finding the median efficiently.

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small = []  # max heap
        self.large = []  # min heap

    def addNum(self, num):
        heapq.heappush(self.small, -num)
        heapq.heappush(self.large, -heapq.heappop(self.small))
        if len(self.large) > len(self.small):
            heapq.heappush(self.small, -heapq.heappop(self.large))

    def findMedian(self):
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2
```

---

### 7. Merge k Sorted Lists.md

**Merge k Sorted Lists**

**Description:**  
Merge k sorted linked lists and return it as one sorted list.

```python
import heapq

def mergeKLists(lists):
    heap = []
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))
    dummy = curr = ListNode()
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    return dummy.next
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
