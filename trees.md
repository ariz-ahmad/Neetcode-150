Here are Markdown files for each “Trees” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Maximum Depth of Binary Tree.md

**Maximum Depth of Binary Tree**

**Description:**  
Given the root of a binary tree, return its maximum depth.

```python
def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```

---

### 2. Same Tree.md

**Same Tree**

**Description:**  
Given two binary trees, check if they are the same.

```python
def isSameTree(p, q):
    if not p and not q:
        return True
    if not p or not q or p.val != q.val:
        return False
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

---

### 3. Invert Binary Tree.md

**Invert Binary Tree**

**Description:**  
Invert a binary tree.

```python
def invertTree(root):
    if root:
        root.left, root.right = invertTree(root.right), invertTree(root.left)
    return root
```

---

### 4. Subtree of Another Tree.md

**Subtree of Another Tree**

**Description:**  
Check if one tree is a subtree of another.

```python
def isSubtree(s, t):
    if not s:
        return False
    if isSameTree(s, t):
        return True
    return isSubtree(s.left, t) or isSubtree(s.right, t)

def isSameTree(s, t):
    if not s and not t:
        return True
    if not s or not t or s.val != t.val:
        return False
    return isSameTree(s.left, t.left) and isSameTree(s.right, t.right)
```

---

### 5. Lowest Common Ancestor of a Binary Search Tree.md

**Lowest Common Ancestor of a Binary Search Tree**

**Description:**  
Given a binary search tree, find the lowest common ancestor of two nodes.

```python
def lowestCommonAncestor(root, p, q):
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
```

---

### 6. Binary Tree Level Order Traversal.md

**Binary Tree Level Order Traversal**

**Description:**  
Return the level order traversal of a binary tree’s nodes’ values.

```python
def levelOrder(root):
    from collections import deque
    res = []
    if not root:
        return res
    q = deque([root])
    while q:
        level = []
        for _ in range(len(q)):
            node = q.popleft()
            level.append(node.val)
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
        res.append(level)
    return res
```

---

### 7. Insert into a Binary Search Tree.md

**Insert into a Binary Search Tree**

**Description:**  
Insert a value into a binary search tree and return the root.

```python
def insertIntoBST(root, val):
    if not root:
        return TreeNode(val)
    if val < root.val:
        root.left = insertIntoBST(root.left, val)
    else:
        root.right = insertIntoBST(root.right, val)
    return root
```

---

### 8. Validate Binary Search Tree.md

**Validate Binary Search Tree**

**Description:**  
Check if a binary tree is a valid binary search tree.

```python
def isValidBST(root):
    def helper(node, left, right):
        if not node:
            return True
        if not (node.val > left and node.val < right):
            return False
        return helper(node.left, left, node.val) and helper(node.right, node.val, right)
    return helper(root, float('-inf'), float('inf'))
```

---

### 9. Kth Smallest Element in a BST.md

**Kth Smallest Element in a BST**

**Description:**  
Find the kth smallest element in a binary search tree.

```python
def kthSmallest(root, k):
    stack = []
    while True:
        while root:
            stack.append(root)
            root = root.left
        root = stack.pop()
        k -= 1
        if k == 0:
            return root.val
        root = root.right
```

---

### 10. Construct Binary Tree from Preorder and Inorder Traversal.md

**Construct Binary Tree from Preorder and Inorder Traversal**

**Description:**  
Given preorder and inorder traversal of a tree, construct the binary tree.

```python
def buildTree(preorder, inorder):
    if not inorder:
        return None
    root = TreeNode(preorder.pop(0))
    idx = inorder.index(root.val)
    root.left = buildTree(preorder, inorder[:idx])
    root.right = buildTree(preorder, inorder[idx+1:])
    return root
```

---

### 11. Binary Tree Maximum Path Sum.md

**Binary Tree Maximum Path Sum**

**Description:**  
Find the maximum path sum in a binary tree.

```python
def maxPathSum(root):
    res = [root.val]
    def dfs(node):
        if not node:
            return 0
        left = max(dfs(node.left), 0)
        right = max(dfs(node.right), 0)
        res[0] = max(res[0], node.val + left + right)
        return node.val + max(left, right)
    dfs(root)
    return res[0]
```

---

### 12. Serialize and Deserialize Binary Tree.md

**Serialize and Deserialize Binary Tree**

**Description:**  
Design an algorithm to serialize and deserialize a binary tree.

```python
class Codec:
    def serialize(self, root):
        vals = []
        def dfs(node):
            if node:
                vals.append(str(node.val))
                dfs(node.left)
                dfs(node.right)
            else:
                vals.append('#')
        dfs(root)
        return ' '.join(vals)

    def deserialize(self, data):
        vals = iter(data.split())
        def dfs():
            val = next(vals)
            if val == '#':
                return None
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node
        return dfs()
```

---

### 13. Flatten Binary Tree to Linked List.md

**Flatten Binary Tree to Linked List**

**Description:**  
Flatten a binary tree to a linked list in-place.

```python
def flatten(root):
    if not root:
        return
    flatten(root.left)
    flatten(root.right)
    if root.left:
        right = root.right
        root.right = root.left
        root.left = None
        curr = root.right
        while curr.right:
            curr = curr.right
        curr.right = right
```

---

### 14. Populating Next Right Pointers in Each Node.md

**Populating Next Right Pointers in Each Node**

**Description:**  
Populate each next pointer to point to its next right node in a perfect binary tree.

```python
def connect(root):
    if not root:
        return None
    leftmost = root
    while leftmost.left:
        head = leftmost
        while head:
            head.left.next = head.right
            if head.next:
                head.right.next = head.next.left
            head = head.next
        leftmost = leftmost.left
    return root
```

---

### 15. Subtree with Maximum Average.md

**Subtree with Maximum Average**

**Description:**  
Find the subtree with the maximum average value.

```python
def findSubtreeWithMaxAverage(root):
    res = [None, float('-inf')]
    def helper(node):
        if not node:
            return (0, 0)
        left_sum, left_count = helper(node.left)
        right_sum, right_count = helper(node.right)
        total_sum = left_sum + right_sum + node.val
        total_count = left_count + right_count + 1
        avg = total_sum / total_count
        if avg > res[1]:
            res[0], res[1] = node, avg
        return (total_sum, total_count)
    helper(root)
    return res[0]
```

---

Let me know if you want the next section or need help combining these files!
