# 3110. Score of a String

**Difficulty:** Easy  
**Topic Tags:** String  
**LeetCode Link:** [https://leetcode.com/problems/score-of-a-string/](https://leetcode.com/problems/score-of-a-string/)

---

## Problem Description

You are given a string `s`. The **score** of a string is defined as the sum of the absolute differences between the **ASCII values** of adjacent characters.

Return the **score** of the string `s`.

### Examples

**Example 1:**
```
Input: s = "hello"
Output: 13
Explanation:
  |104 - 101| = 3   (h → e)
  |101 - 108| = 7   (e → l)
  |108 - 108| = 0   (l → l)
  |108 - 111| = 3   (l → o)
  Total = 3 + 7 + 0 + 3 = 13
```

**Example 2:**
```
Input: s = "zaz"
Output: 50
Explanation:
  |122 - 97| = 25   (z → a)
  |97 - 122| = 25   (a → z)
  Total = 25 + 25 = 50
```

### Constraints

- `2 <= s.length <= 100`
- `s` consists only of lowercase English letters.

---

## Approach — ASCII Conversion + Linear Scan

The solution converts each character to its ASCII value using `ord()`, stores them in an array, then iterates through adjacent pairs to accumulate their absolute differences.

### Key Observations

- `ord(c)` returns the ASCII integer value of character `c` (e.g. `ord('a') = 97`, `ord('z') = 122`).
- The absolute difference between two values can be computed as `max(a, b) - min(a, b)`, which always yields a non-negative result.
- A single pass through adjacent pairs is all that's needed — no sorting or nested loops required.

### Step-by-Step

1. **Convert to ASCII** — iterate through `s` and append `ord(i)` for each character into `arr`.
2. **Scan adjacent pairs** — for each index `x` from `0` to `len(arr) - 2`, compute `max - min` of the pair.
3. **Accumulate** — add each difference to `sum` and return the total.

### Complexity

| | Complexity |
|---|---|
| **Time** | O(n) — one pass to build the array, one pass to sum differences |
| **Space** | O(n) — an auxiliary array stores all ASCII values |

---

## Solution

```python
class Solution(object):
    def scoreOfString(self, s):
        sum = 0
        difference = 0
        arr = []
        for i in s:
            arr.append(ord(i))
        for x in range(len(arr) - 1):
            difference = max(arr[x], arr[x + 1]) - min(arr[x], arr[x + 1])
            sum = sum + difference
        return sum
```

> **Note:** The `print(arr)` statement in the original solution is a debug line and has no effect on the result. It can safely be removed for submission.

---

## Walkthrough

**Example 1:** `s = "hello"`

**Step 1 — Build ASCII array:**

| Character | h | e | l | l | o |
|-----------|-----|-----|-----|-----|-----|
| ASCII | 104 | 101 | 108 | 108 | 111 |

```
arr = [104, 101, 108, 108, 111]
```

**Step 2 — Sum adjacent differences:**

| Pair | Calculation | Difference |
|------|-------------|------------|
| h → e | max(104, 101) - min(104, 101) = 104 - 101 | 3 |
| e → l | max(101, 108) - min(101, 108) = 108 - 101 | 7 |
| l → l | max(108, 108) - min(108, 108) = 108 - 108 | 0 |
| l → o | max(108, 111) - min(108, 111) = 111 - 108 | 3 |

```
sum = 3 + 7 + 0 + 3 = 13
```

✅ Output: `13`

---

## Alternative Approach — One-liner with `abs()` (O(n))

The same result can be achieved more concisely using `abs()` and `zip()`, avoiding the need for an auxiliary array entirely:

```python
class Solution(object):
    def scoreOfString(self, s):
        return sum(abs(ord(a) - ord(b)) for a, b in zip(s, s[1:]))
```

`zip(s, s[1:])` pairs each character with the next one, and `abs()` cleanly handles the absolute difference without needing `max` and `min`. Both approaches produce identical results.
