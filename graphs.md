Here are Markdown files for each “Graphs” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Number of Islands.md

**Number of Islands**

**Description:**  
Given a 2D grid map of '1's (land) and '0's (water), count the number of islands.

```python
def numIslands(grid):
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    visited = set()
    def dfs(r, c):
        if (r < 0 or c < 0 or r >= rows or c >= cols or
            grid[r][c] == '0' or (r, c) in visited):
            return
        visited.add((r, c))
        dfs(r+1, c)
        dfs(r-1, c)
        dfs(r, c+1)
        dfs(r, c-1)
    count = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1' and (r, c) not in visited:
                dfs(r, c)
                count += 1
    return count
```

---

### 2. Clone Graph.md

**Clone Graph**

**Description:**  
Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph.

```python
def cloneGraph(node):
    if not node:
        return None
    old_to_new = {}
    def dfs(n):
        if n in old_to_new:
            return old_to_new[n]
        copy = Node(n.val)
        old_to_new[n] = copy
        for neighbor in n.neighbors:
            copy.neighbors.append(dfs(neighbor))
        return copy
    return dfs(node)
```

---

### 3. Course Schedule.md

**Course Schedule**

**Description:**  
There are a total of numCourses courses you have to take, labeled from 0 to numCourses-1. Some courses may have prerequisites. Return true if it is possible to finish all courses.

```python
def canFinish(numCourses, prerequisites):
    from collections import defaultdict, deque
    graph = defaultdict(list)
    indegree = [0] * numCourses
    for a, b in prerequisites:
        graph[b].append(a)
        indegree[a] += 1
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    count = 0
    while queue:
        node = queue.popleft()
        count += 1
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    return count == numCourses
```

---

### 4. Pacific Atlantic Water Flow.md

**Pacific Atlantic Water Flow**

**Description:**  
Given an m x n matrix of non-negative integers representing the height of each unit cell, return a list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

```python
def pacificAtlantic(heights):
    if not heights:
        return []
    rows, cols = len(heights), len(heights[0])
    pac, atl = set(), set()
    def dfs(r, c, visit, prev):
        if (r < 0 or c < 0 or r >= rows or c >= cols or
            (r, c) in visit or heights[r][c] < prev):
            return
        visit.add((r, c))
        dfs(r+1, c, visit, heights[r][c])
        dfs(r-1, c, visit, heights[r][c])
        dfs(r, c+1, visit, heights[r][c])
        dfs(r, c-1, visit, heights[r][c])
    for c in range(cols):
        dfs(0, c, pac, heights[0][c])
        dfs(rows-1, c, atl, heights[rows-1][c])
    for r in range(rows):
        dfs(r, 0, pac, heights[r][0])
        dfs(r, cols-1, atl, heights[r][cols-1])
    return list(pac & atl)
```

---

### 5. Number of Connected Components in an Undirected Graph.md

**Number of Connected Components in an Undirected Graph**

**Description:**  
Given n nodes and a list of edges, return the number of connected components in the undirected graph.

```python
def countComponents(n, edges):
    from collections import defaultdict
    graph = defaultdict(list)
    for a, b in edges:
        graph[a].append(b)
        graph[b].append(a)
    visited = set()
    def dfs(node):
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                dfs(neighbor)
    count = 0
    for i in range(n):
        if i not in visited:
            visited.add(i)
            dfs(i)
            count += 1
    return count
```

---

### 6. Graph Valid Tree.md

**Graph Valid Tree**

**Description:**  
Given n nodes labeled from 0 to n-1 and a list of edges, check if the edges make up a valid tree.

```python
def validTree(n, edges):
    if len(edges) != n - 1:
        return False
    from collections import defaultdict
    graph = defaultdict(list)
    for a, b in edges:
        graph[a].append(b)
        graph[b].append(a)
    visited = set()
    def dfs(node, parent):
        for neighbor in graph[node]:
            if neighbor == parent:
                continue
            if neighbor in visited or not dfs(neighbor, node):
                return False
        return True
    visited.add(0)
    return dfs(0, -1) and len(visited) == n
```

---

### 7. Word Ladder.md

**Word Ladder**

**Description:**  
Given two words, beginWord and endWord, and a dictionary, return the length of the shortest transformation sequence from beginWord to endWord.

```python
def ladderLength(beginWord, endWord, wordList):
    from collections import deque
    wordSet = set(wordList)
    if endWord not in wordSet:
        return 0
    queue = deque([(beginWord, 1)])
    while queue:
        word, length = queue.popleft()
        if word == endWord:
            return length
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + c + word[i+1:]
                if next_word in wordSet:
                    wordSet.remove(next_word)
                    queue.append((next_word, length + 1))
    return 0
```

---

### 8. Reconstruct Itinerary.md

**Reconstruct Itinerary**

**Description:**  
Given a list of airline tickets, reconstruct the itinerary in lexical order.

```python
def findItinerary(tickets):
    from collections import defaultdict
    graph = defaultdict(list)
    for a, b in sorted(tickets, reverse=True):
        graph[a].append(b)
    res = []
    def visit(airport):
        while graph[airport]:
            visit(graph[airport].pop())
        res.append(airport)
    visit('JFK')
    return res[::-1]
```

---

### 9. Course Schedule II.md

**Course Schedule II**

**Description:**  
Return the order in which you should take courses to finish all courses given the prerequisites.

```python
def findOrder(numCourses, prerequisites):
    from collections import defaultdict, deque
    graph = defaultdict(list)
    indegree = [0] * numCourses
    for a, b in prerequisites:
        graph[b].append(a)
        indegree[a] += 1
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    res = []
    while queue:
        node = queue.popleft()
        res.append(node)
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    return res if len(res) == numCourses else []
```

---

### 10. Alien Dictionary.md

**Alien Dictionary**

**Description:**  
Given a list of words sorted lexicographically by the rules of an alien language, return a possible order of the alphabet.

```python
def alienOrder(words):
    from collections import defaultdict, deque
    graph = defaultdict(set)
    indegree = {}
    for word in words:
        for c in word:
            indegree[c] = 0
    for i in range(len(words) - 1):
        w1, w2 = words[i], words[i+1]
        min_len = min(len(w1), len(w2))
        if w1[:min_len] == w2[:min_len] and len(w1) > len(w2):
            return ""
        for j in range(min_len):
            if w1[j] != w2[j]:
                if w2[j] not in graph[w1[j]]:
                    graph[w1[j]].add(w2[j])
                    indegree[w2[j]] += 1
                break
    queue = deque([c for c in indegree if indegree[c] == 0])
    res = []
    while queue:
        c = queue.popleft()
        res.append(c)
        for nei in graph[c]:
            indegree[nei] -= 1
            if indegree[nei] == 0:
                queue.append(nei)
    return "".join(res) if len(res) == len(indegree) else ""
```

---

### 11. Redundant Connection.md

**Redundant Connection**

**Description:**  
In a tree with n nodes, one additional edge is added. Find the edge that can be removed so that the resulting graph is a tree.

```python
def findRedundantConnection(edges):
    parent = [i for i in range(len(edges) + 1)]
    def find(x):
        while parent[x] != x:
            parent[x] = parent[parent[x]]
            x = parent[x]
        return x
    for u, v in edges:
        pu, pv = find(u), find(v)
        if pu == pv:
            return [u, v]
        parent[pu] = pv
```

---

### 12. Critical Connections in a Network.md

**Critical Connections in a Network**

**Description:**  
Given a network of n servers, find all critical connections in the network.

```python
def criticalConnections(n, connections):
    from collections import defaultdict
    graph = defaultdict(list)
    for a, b in connections:
        graph[a].append(b)
        graph[b].append(a)
    res = []
    disc = [None] * n
    low = [None] * n
    time = [0]
    def dfs(u, parent):
        disc[u] = low[u] = time[0]
        time[0] += 1
        for v in graph[u]:
            if disc[v] is None:
                dfs(v, u)
                low[u] = min(low[u], low[v])
                if low[v] > disc[u]:
                    res.append([u, v])
            elif v != parent:
                low[u] = min(low[u], disc[v])
    for i in range(n):
        if disc[i] is None:
            dfs(i, -1)
    return res
```

---

### 13. Graph Valid Path.md

**Graph Valid Path**

**Description:**  
Given an undirected graph, determine if there is a valid path between two nodes.

```python
def validPath(n, edges, source, destination):
    from collections import defaultdict, deque
    graph = defaultdict(list)
    for a, b in edges:
        graph[a].append(b)
        graph[b].append(a)
    visited = set()
    queue = deque([source])
    while queue:
        node = queue.popleft()
        if node == destination:
            return True
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return source == destination
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 1 license type
