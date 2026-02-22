# 70. Climbing Stairs

**Difficulty:** Easy  
**Topic Tags:** Math, Dynamic Programming, Memoization  
**LeetCode Link:** [https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)

---

## Problem Description

You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

### Examples

**Example 1:**
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

### Constraints

- `1 <= n <= 45`

---

## Approach — Dynamic Programming (Fibonacci Sequence)

This problem is essentially asking us to compute the **n-th Fibonacci number**.

### Key Observations

- To reach step `n`, you must have come from either step `n-1` (1 step) or step `n-2` (2 steps).
- Therefore: `ways(n) = ways(n-1) + ways(n-2)`
- This is exactly the Fibonacci recurrence.
- Base cases: `ways(1) = 1`, `ways(2) = 2`
- Instead of storing the entire DP array, we only need the **last two values** at any time, keeping space constant.

### Fibonacci Pattern

| n | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| ways | 1 | 2 | 3 | 5 | 8 | 13 |

### Complexity

| | Complexity |
|---|---|
| **Time** | O(n) |
| **Space** | O(1) |

---

## Solution

```python
class Solution(object):
    def climbStairs(self, n):
        if n <= 2:
            return n

        a, b = 1, 2   # ways(1), ways(2)
        for _ in range(3, n + 1):
            a, b = b, a + b   # update

        return b
```

---

## Walkthrough — Example: n = 5

We start with `a = 1` (ways to reach step 1) and `b = 2` (ways to reach step 2), then iterate from step 3 up to n:

| Step | a (prev) | b (curr) | Calculation |
|------|----------|----------|-------------|
| 3 | 1 | 2 | b = 1 + 2 = **3** |
| 4 | 2 | 3 | b = 2 + 3 = **5** |
| 5 | 3 | 5 | b = 3 + 5 = **8** |

✅ Output: `8`
