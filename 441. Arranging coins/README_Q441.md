# 441. Arranging Coins

**Difficulty:** Easy  
**Topic Tags:** Math, Binary Search  
**LeetCode Link:** [https://leetcode.com/problems/arranging-coins/](https://leetcode.com/problems/arranging-coins/)

---

## Problem Description

You have `n` coins and you want to build a staircase with these coins. The staircase consists of `k` rows where the `i`-th row has exactly `i` coins. The last row of the staircase **may be incomplete**.

Given the integer `n`, return the number of **complete rows** of the staircase you will build.

### Examples

**Example 1:**
```
Input: n = 5
Output: 2

    ¤
   ¤ ¤
  ¤ ¤ _

Explanation: The 3rd row only has 2 coins, which is incomplete. So 2 complete rows are returned.
```

**Example 2:**
```
Input: n = 8
Output: 3

    ¤
   ¤ ¤
  ¤ ¤ ¤
 ¤ ¤ _ _

Explanation: The 4th row only has 2 coins, which is incomplete. So 3 complete rows are returned.
```

### Constraints

- `1 <= n <= 2³¹ - 1`

---

## Approach — Linear Simulation

The solution simulates filling each row one at a time. Starting from row 1, it subtracts the number of coins needed for each row from `n`. As long as `n` remains non-negative, the row is considered complete. Once `n` goes negative, the loop exits and we return `nrows - 1` (subtracting the last incomplete row we attempted).

### Key Observations

- Row `i` requires exactly `i` coins to be complete.
- We keep a running count `nrows`, incrementing it each iteration and subtracting it from `n`.
- The loop exits when `n < 0`, meaning the current row couldn't be fully filled.
- We return `nrows - 1` because the last row that caused `n` to go negative was not complete.

### Complexity

| | Complexity |
|---|---|
| **Time** | O(√n) — the number of complete rows grows roughly as the square root of `n` |
| **Space** | O(1) — only two variables are used |

---

## Solution

```python
class Solution(object):
    def arrangeCoins(self, n):
        nrows = 0
        while n >= 0:
            nrows = nrows + 1
            n = n - nrows
        return nrows - 1
```

---

## Walkthrough

**Example 1:** `n = 5`

| Iteration | nrows | Coins used (n - nrows) | n remaining |
|-----------|-------|------------------------|-------------|
| 1 | 1 | 5 - 1 = 4 | 4 |
| 2 | 2 | 4 - 2 = 2 | 2 |
| 3 | 3 | 2 - 3 = -1 | -1 |

`n` goes negative at row 3 → loop exits → return `nrows - 1 = 3 - 1`

✅ Output: `2`

---

**Example 2:** `n = 8`

| Iteration | nrows | Coins used (n - nrows) | n remaining |
|-----------|-------|------------------------|-------------|
| 1 | 1 | 8 - 1 = 7 | 7 |
| 2 | 2 | 7 - 2 = 5 | 5 |
| 3 | 3 | 5 - 3 = 2 | 2 |
| 4 | 4 | 2 - 4 = -2 | -2 |

`n` goes negative at row 4 → loop exits → return `nrows - 1 = 4 - 1`

✅ Output: `3`

---

## Alternative Approach — Math Formula (O(1))

The total number of coins to fill `k` complete rows is the triangular number `k * (k + 1) / 2`. Solving for `k` using the quadratic formula gives a direct O(1) solution:

```python
import math

class Solution(object):
    def arrangeCoins(self, n):
        return int((-1 + math.sqrt(1 + 8 * n)) / 2)
```

This skips iteration entirely by solving `k(k+1)/2 = n` directly for `k`, making it the most efficient approach for very large values of `n`.
