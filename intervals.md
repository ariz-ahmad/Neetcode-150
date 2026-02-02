Here are Markdown files for each “Intervals” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Insert Interval.md

**Insert Interval**

**Description:**  
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

```python
def insert(intervals, newInterval):
    res = []
    for i in range(len(intervals)):
        if newInterval[1] < intervals[i][0]:
            res.append(newInterval)
            return res + intervals[i:]
        elif newInterval[0] > intervals[i][1]:
            res.append(intervals[i])
        else:
            newInterval[0] = min(newInterval[0], intervals[i][0])
            newInterval[1] = max(newInterval[1], intervals[i][1])
    res.append(newInterval)
    return res
```

---

### 2. Merge Intervals.md

**Merge Intervals**

**Description:**  
Given an array of intervals, merge all overlapping intervals.

```python
```python
```python
```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    res = []
    for interval in intervals:
        if not res or res[-1][1] < interval[0]:
            res.append(interval)
        else:
            res[-1][1] = max(res[-1][1], interval[1])
    return res
```

---

### 3. Non-overlapping Intervals.md

**Non-overlapping Intervals**

**Description:**  
Given an array of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

```python
def eraseOverlapIntervals(intervals):
    intervals.sort(key=lambda x: x[1])
    res, end = 0, float('-inf')
    for interval in intervals:
        if interval[0] >= end:
            end = interval[1]
        else:
            res += 1
    return res
```

---

### 4. Meeting Rooms.md

**Meeting Rooms**

**Description:**  
Given an array of meeting time intervals, determine if a person could attend all meetings.

```python
def canAttendMeetings(intervals):
    intervals.sort(key=lambda x: x[0])
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i-1][1]:
            return False
    return True
```

---

### 5. Meeting Rooms II.md

**Meeting Rooms II**

**Description:**  
Given an array of meeting time intervals, return the minimum number of conference rooms required.

```python
import heapq

def minMeetingRooms(intervals):
    if not intervals:
        return 0
    intervals.sort(key=lambda x: x[0])
    heap = [intervals[0][1]]
    for i in range(1, len(intervals)):
        if intervals[i][0] >= heap[0]:
            heapq.heappop(heap)
        heapq.heappush(heap, intervals[i][1])
    return len(heap)
```

---

### 6. Minimum Interval to Include Each Query.md

**Minimum Interval to Include Each Query**

**Description:**  
You are given a 2D array of intervals and an array of queries. For each query, return the size of the smallest interval that contains the query.

```python
import heapq

def minInterval(intervals, queries):
    intervals.sort()
    res, heap, i = {}, [], 0
    sorted_queries = sorted((q, idx) for idx, q in enumerate(queries))
    for q, idx in sorted_queries:
        while i < len(intervals) and intervals[i][0] <= q:
            l, r = intervals[i]
            heapq.heappush(heap, (r - l + 1, r))
            i += 1
        while heap and heap[0][1] < q:
            heapq.heappop(heap)
        res[idx] = heap[0][0] if heap else -1
    return [res[i] for i in range(len(queries))]
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
