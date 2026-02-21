# 69. Sqrt(x)

**Difficulty:** Easy  
**Topic Tags:** Math, Binary Search  
**LeetCode Link:** [https://leetcode.com/problems/sqrtx/](https://leetcode.com/problems/sqrtx/)

---

## Problem Description

Given a non-negative integer `x`, return the square root of `x` rounded down to the nearest integer. The returned integer should be non-negative as well.

You **must not** use any built-in exponent function or operator (e.g. `pow(x, 0.5)` in Python or `x ** 0.5`).

### Examples

**Example 1:**
```
Input: x = 4
Output: 2
```

**Example 2:**
```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.828..., so we return 2 (floored).
```

### Constraints

- `0 <= x <= 2³¹ - 1`

---

## Approach — Binary Search

Instead of computing the exact square root, we can use **binary search** to find the largest integer `mid` such that `mid * mid <= x`.

### Key Observations

- For `x < 2`, the answer is `x` itself (handles `0` and `1`).
- The square root of any `x >= 2` always lies between `1` and `x // 2`, so we search in that range.
- We narrow the range by comparing `mid * mid` with `x`:
  - If equal → exact root found, return `mid`.
  - If less → root is larger, move `left` up.
  - If greater → root is smaller, move `right` down.
- When the loop ends, `right` holds the floored square root.

### Complexity

| | Complexity |
|---|---|
| **Time** | O(log n) |
| **Space** | O(1) |

---

## Solution

```python
class Solution(object):
    def mySqrt(self, x):
        if x < 2:
            return x

        left, right = 1, x // 2

        while left <= right:
            mid = (left + right) // 2
            sq = mid * mid

            if sq == x:
                return mid
            elif sq < x:
                left = mid + 1
            else:
                right = mid - 1

        return right
```

---

## Walkthrough — Example: x = 8

| Iteration | left | right | mid | mid² | Action |
|-----------|------|-------|-----|------|--------|
| 1 | 1 | 4 | 2 | 4 | 4 < 8 → left = 3 |
| 2 | 3 | 4 | 3 | 9 | 9 > 8 → right = 2 |
| End | 3 | 2 | — | — | left > right, return right = **2** |

✅ Output: `2`
