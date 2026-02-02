Here are Markdown files for each “Advanced Graphs” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Course Schedule III.md

**Course Schedule III**

**Description:**  
There are n different online courses. Each course has a duration and a last day by which you must finish it. Return the maximum number of courses you can take.

```python
import heapq

def scheduleCourse(courses):
    courses.sort(key=lambda x: x[1])
    heap = []
    total = 0
    for duration, lastDay in courses:
        total += duration
        heapq.heappush(heap, -duration)
        if total > lastDay:
            total += heapq.heappop(heap)
    return len(heap)
```

---

### 2. Network Delay Time.md

**Network Delay Time**

**Description:**  
You are given a network of n nodes, times[i] = (u, v, w) means a signal travels from u to v in w time. Return the time it takes for all nodes to receive the signal from a starting node k.

```python
import heapq
from collections import defaultdict

def networkDelayTime(times, n, k):
    graph = defaultdict(list)
    for u, v, w in times:
        graph[u].append((v, w))
    heap = [(0, k)]
    dist = {}
    while heap:
        time, node = heapq.heappop(heap)
        if node in dist:
            continue
        dist[node] = time
        for nei, wt in graph[node]:
            if nei not in dist:
                heapq.heappush(heap, (time + wt, nei))
    return max(dist.values()) if len(dist) == n else -1
```

---

### 3. Minimum Cost to Connect All Points.md

**Minimum Cost to Connect All Points**

**Description:**  
Given points in a 2D plane, return the minimum cost to connect all points such that there is exactly one simple path between any two points.

```python
import heapq

def minCostConnectPoints(points):
    n = len(points)
    visited = set()
    minHeap = [(0, 0)]
    res = 0
    while len(visited) < n:
        cost, i = heapq.heappop(minHeap)
        if i in visited:
            continue
        res += cost
        visited.add(i)
        for j in range(n):
            if j not in visited:
                dist = abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1])
                heapq.heappush(minHeap, (dist, j))
    return res
```

---

### 4. Swim in Rising Water.md

**Swim in Rising Water**

**Description:**  
Given an n x n integer matrix grid, return the least time required to swim from the top left to the bottom right.

```python
import heapq

def swimInWater(grid):
    n = len(grid)
    visited = set()
    minHeap = [(grid[0][0], 0, 0)]
    directions = [(0,1),(1,0),(-1,0),(0,-1)]
    while minHeap:
        time, r, c = heapq.heappop(minHeap)
        if (r, c) == (n-1, n-1):
            return time
        visited.add((r, c))
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < n and 0 <= nc < n and (nr, nc) not in visited:
                heapq.heappush(minHeap, (max(time, grid[nr][nc]), nr, nc))
```

---

### 5. Cheapest Flights Within K Stops.md

**Cheapest Flights Within K Stops**

**Description:**  
Given n cities and flights, find the cheapest price from src to dst with at most k stops.

```python
import heapq
from collections import defaultdict

def findCheapestPrice(n, flights, src, dst, k):
    graph = defaultdict(list)
    for u, v, w in flights:
        graph[u].append((v, w))
    heap = [(0, src, 0)]
    while heap:
        cost, node, stops = heapq.heappop(heap)
        if node == dst:
            return cost
        if stops > k:
            continue
        for nei, wt in graph[node]:
            heapq.heappush(heap, (cost + wt, nei, stops + 1))
    return -1
```

---

### 6. Redundant Connection II.md

**Redundant Connection II**

**Description:**  
In a directed graph, one additional edge is added. Find the edge that can be removed so that the resulting graph is a rooted tree.

```python
def findRedundantDirectedConnection(edges):
    parent = {}
    candA = candB = None
    for u, v in edges:
        if v in parent:
            candA = [parent[v], v]
            candB = [u, v]
            break
        parent[v] = u

    def find(u, parents):
        while parents[u] != u:
            parents[u] = parents[parents[u]]
            u = parents[u]
        return u

    n = len(edges)
    parents = [i for i in range(n + 1)]
    for u, v in edges:
        if [u, v] == candB:
            continue
        pu, pv = find(u, parents), find(v, parents)
        if pu == pv:
            if candA:
                return candA
            return [u, v]
        parents[pv] = pu
    return candB
```

---

Let me know if you want the next section or need help combining these files!
