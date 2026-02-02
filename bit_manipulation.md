Here are Markdown files for each “Bit Manipulation” problem from NeetCode 150 in Python, with a brief description and a full solution. Save each block as its own `.md` file, named as shown.

---

### 1. Single Number.md

**Single Number**

**Description:**  
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

```python
def singleNumber(nums):
    res = 0
    for n in nums:
        res ^= n
    return res
```

---

### 2. Number of 1 Bits.md

**Number of 1 Bits**

**Description:**  
Write a function that takes an unsigned integer and returns the number of '1' bits it has.

```python
def hammingWeight(n):
    res = 0
    while n:
        n &= n - 1
        res += 1
    return res
```

---

### 3. Counting Bits.md

**Counting Bits**

**Description:**  
Given a non-negative integer n, return an array of the number of 1's in the binary representation of every number in the range [0, n].

```python
def countBits(n):
    res = [0] * (n + 1)
    for i in range(1, n + 1):
        res[i] = res[i >> 1] + (i & 1)
    return res
```

---

### 4. Reverse Bits.md

**Reverse Bits**

**Description:**  
Reverse bits of a given 32 bits unsigned integer.

```python
def reverseBits(n):
    res = 0
    for _ in range(32):
        res = (res << 1) | (n & 1)
        n >>= 1
    return res
```

---

### 5. Missing Number.md

**Missing Number**

**Description:**  
Given an array containing n distinct numbers in the range [0, n], return the one that is missing from the array.

```python
def missingNumber(nums):
    res = len(nums)
    for i, n in enumerate(nums):
        res ^= i ^ n
    return res
```

---

### 6. Sum of Two Integers.md

**Sum of Two Integers**

**Description:**  
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

```python
def getSum(a, b):
    MASK = 0xFFFFFFFF
    MAX = 0x7FFFFFFF
    while b != 0:
        a, b = (a ^ b) & MASK, ((a & b) << 1) & MASK
    return a if a <= MAX else ~(a ^ MASK)
```

---

### 7. Reverse Integer.md

**Reverse Integer**

**Description:**  
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range, return 0.

```python
def reverse(x):
    sign = -1 if x < 0 else 1
    x *= sign
    res = 0
    while x:
        res = res * 10 + x % 10
        x //= 10
    res *= sign
    if res < -2**31 or res > 2**31 - 1:
        return 0
    return res
```

---

Let me know if you want the next section or need help combining these files!
