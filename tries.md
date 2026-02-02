Here are Markdown files for each “Tries” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Implement Trie (Prefix Tree).md

**Implement Trie (Prefix Tree)**

**Description:**  
Design and implement a Trie (prefix tree) with insert, search, and startsWith methods.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_end = True

    def search(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                return False
            node = node.children[c]
        return node.is_end

    def startsWith(self, prefix):
        node = self.root
        for c in prefix:
            if c not in node.children:
                return False
            node = node.children[c]
        return True
```

---

### 2. Design Add and Search Words Data Structure.md

**Design Add and Search Words Data Structure**

**Description:**  
Design a data structure that supports adding new words and finding if a string matches any previously added string, with support for '.' as a wildcard character.

```python
class WordDictionary:
    def __init__(self):
        self.root = {}

    def addWord(self, word):
        node = self.root
        for c in word:
            if c not in node:
                node[c] = {}
            node = node[c]
        node['#'] = True

    def search(self, word):
        def dfs(j, node):
            for i in range(j, len(word)):
                c = word[i]
                if c == '.':
                    return any(dfs(i+1, node[x]) for x in node if x != '#')
                if c not in node:
                    return False
                node = node[c]
            return '#' in node
        return dfs(0, self.root)
```

---

### 3. Word Search II.md

**Word Search II**

**Description:**  
Given an m x n board of characters and a list of words, return all words on the board.

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.word = None

def findWords(board, words):
    root = TrieNode()
    for word in words:
        node = root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.word = word

    rows, cols = len(board), len(board[0])
    res = []

    def dfs(r, c, node):
        if (r < 0 or c < 0 or r >= rows or c >= cols or
            board[r][c] not in node.children):
            return
        char = board[r][c]
        node = node.children[char]
        if node.word:
            res.append(node.word)
            node.word = None
        board[r][c] = '#'
        for dr, dc in [(-1,0),(1,0),(0,-1),(0,1)]:
            dfs(r+dr, c+dc, node)
        board[r][c] = char

    for r in range(rows):
        for c in range(cols):
            dfs(r, c, root)
    return res
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 2 license types
