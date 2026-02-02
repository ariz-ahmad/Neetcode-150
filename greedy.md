Here are Markdown files for each “Greedy” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Jump Game.md

**Jump Game**

**Description:**  
Given an array of non-negative integers, return true if you can reach the last index.

```python
def canJump(nums):
    goal = len(nums) - 1
    for i in range(len(nums) - 2, -1, -1):
        if i + nums[i] >= goal:
            goal = i
    return goal == 0
```

---

### 2. Gas Station.md

**Gas Station**

**Description:**  
Given two integer arrays gas and cost, return the starting gas station’s index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

```python
def canCompleteCircuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1
    total, start = 0, 0
    for i in range(len(gas)):
        total += gas[i] - cost[i]
        if total < 0:
            start = i + 1
            total = 0
    return start
```

---

### 3. Candy.md

**Candy**

**Description:**  
There are n children standing in a line. Each child is assigned a rating value. Distribute candies to children such that each child has at least one candy, and children with a higher rating get more candies than their neighbors.

```python
def candy(ratings):
    n = len(ratings)
    candies = [1] * n
    for i in range(1, n):
        if ratings[i] > ratings[i-1]:
            candies[i] = candies[i-1] + 1
    for i in range(n-2, -1, -1):
        if ratings[i] > ratings[i+1]:
            candies[i] = max(candies[i], candies[i+1] + 1)
    return sum(candies)
```

---

### 4. Insert Interval.md

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

### 5. Merge Intervals.md

**Merge Intervals**

**Description:**  
Given an array of intervals, merge all overlapping intervals.

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

### 6. Non-overlapping Intervals.md

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

### 7. Partition Labels.md

**Partition Labels**

**Description:**  
A string S of lowercase English letters is given. Partition the string into as many parts as possible so that each letter appears in at most one part.

```python
def partitionLabels(s):
    last = {c: i for i, c in enumerate(s)}
    res = []
    j = anchor = 0
    for i, c in enumerate(s):
        j = max(j, last[c])
        if i == j:
            res.append(i - anchor + 1)
            anchor = i + 1
    return res
```

---

### 8. Queue Reconstruction by Height.md

**Queue Reconstruction by Height**

**Description:**  
Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height and k is the number of people in front who have a height greater than or equal to h. Reconstruct the queue.

```python
def reconstructQueue(people):
    people.sort(key=lambda x: (-x[0], x[1]))
    res = []
    for p in people:
        res.insert(p[1], p)
    return res
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
