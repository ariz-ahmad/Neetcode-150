Here are Markdown files for each “Stack” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Valid Parentheses.md

**Valid Parentheses**

**Description:**  
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

```python
def isValid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in mapping.values():
            stack.append(char)
        elif char in mapping:
            if not stack or stack.pop() != mapping[char]:
                return False
        else:
            return False
    return not stack
```

---

### 2. Min Stack.md

**Min Stack**

**Description:**  
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val):
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self):
        if self.stack.pop() == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]
```

---

### 3. Evaluate Reverse Polish Notation.md

**Evaluate Reverse Polish Notation**

**Description:**  
Evaluate the value of an arithmetic expression in Reverse Polish Notation.

```python
def evalRPN(tokens):
    stack = []
    for token in tokens:
        if token not in "+-*/":
            stack.append(int(token))
        else:
            b, a = stack.pop(), stack.pop()
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            else:
                stack.append(int(a / b))
    return stack[0]
```

---

### 4. Generate Parentheses.md

**Generate Parentheses**

**Description:**  
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

```python
def generateParenthesis(n):
    res = []
    def backtrack(s='', left=0, right=0):
        if len(s) == 2 * n:
            res.append(s)
            return
        if left < n:
            backtrack(s + '(', left + 1, right)
        if right < left:
            backtrack(s + ')', left, right + 1)
    backtrack()
    return res
```

---

### 5. Daily Temperatures.md

**Daily Temperatures**

**Description:**  
Given a list of daily temperatures, return a list such that, for each day, tells you how many days you would have to wait until a warmer temperature.

```python
def dailyTemperatures(temperatures):
    res = [0] * len(temperatures)
    stack = []
    for i, t in enumerate(temperatures):
        while stack and t > temperatures[stack[-1]]:
            idx = stack.pop()
            res[idx] = i - idx
        stack.append(i)
    return res
```

---

### 6. Car Fleet.md

**Car Fleet**

**Description:**  
There are n cars going to the same destination. Each car starts at a different position and speed. Return the number of car fleets that will arrive at the destination.

```python
def carFleet(target, position, speed):
    pair = sorted(zip(position, speed))
    times = [(target - p) / s for p, s in pair]
    res = 0
    while times:
        lead = times.pop()
        res += 1
        while times and times[-1] <= lead:
            times.pop()
    return res
```

---

Let me know if you want the next section or need help combining these files!

Similar code found with 2 license types
