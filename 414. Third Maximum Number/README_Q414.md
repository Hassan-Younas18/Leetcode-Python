# 414. Third Maximum Number

**Difficulty:** Easy  
**Topic Tags:** Array, Sorting  
**LeetCode Link:** [https://leetcode.com/problems/third-maximum-number/](https://leetcode.com/problems/third-maximum-number/)

---

## Problem Description

Given an integer array `nums`, return the **third distinct maximum** number in this array. If the third maximum does not exist, return the **maximum** number.

### Examples

**Example 1:**
```
Input: nums = [3, 2, 1]
Output: 1
Explanation: The third distinct maximum is 1.
```

**Example 2:**
```
Input: nums = [1, 2]
Output: 2
Explanation: The third distinct maximum does not exist, so the maximum (2) is returned.
```

**Example 3:**
```
Input: nums = [2, 2, 3, 1]
Output: 1
Explanation: Note that the third distinct maximum here means the third distinct value.
Both 2's are counted together, so [3, 2, 1] are the three distinct values, and the third is 1.
```

### Constraints

- `1 <= nums.length <= 10⁴`
- `-2³¹ <= nums[i] <= 2³¹ - 1`

---

## Approach — Deduplication + Sorting

The key challenge here is handling **duplicate values** — the problem asks for the third distinct maximum, not just the third element. The solution tackles this in two clean steps: remove duplicates, then sort.

### Key Observations

- `dict.fromkeys(nums)` preserves insertion order while removing duplicates, and wrapping it in `list()` gives us a clean deduplicated array.
- After sorting in descending order, the third distinct maximum is simply at index `2`.
- If fewer than 3 distinct values exist, `sortarr[0]` returns the overall maximum as required.

### Step-by-Step

1. **Deduplicate** — convert `nums` to a list with unique values only using `dict.fromkeys()`.
2. **Sort descending** — sort the deduplicated list from largest to smallest.
3. **Return result** — if 3+ distinct values exist return index `2`, otherwise return index `0` (the maximum).

### Complexity

| | Complexity |
|---|---|
| **Time** | O(n log n) — dominated by the sorting step |
| **Space** | O(n) — a new deduplicated list is created |

---

## Solution

```python
class Solution(object):
    def thirdMax(self, nums):
        sortarr = list(dict.fromkeys(nums))
        sortarr = sorted(sortarr, reverse=True)
        if len(sortarr) >= 3:
            return sortarr[2]
        else:
            return sortarr[0]
```

---

## Walkthrough

**Example 1:** `nums = [2, 2, 3, 1]`

```
Step 1 — Deduplicate:
dict.fromkeys([2, 2, 3, 1]) → [2, 3, 1]

Step 2 — Sort descending:
sorted([2, 3, 1], reverse=True) → [3, 2, 1]

Step 3 — Check length:
len([3, 2, 1]) = 3 → 3 >= 3 ✅ → return sortarr[2]
```
✅ Output: `1`

---

**Example 2:** `nums = [1, 2]`

```
Step 1 — Deduplicate:
dict.fromkeys([1, 2]) → [1, 2]

Step 2 — Sort descending:
sorted([1, 2], reverse=True) → [2, 1]

Step 3 — Check length:
len([2, 1]) = 2 → 2 < 3 ❌ → return sortarr[0]
```
✅ Output: `2`

---

## Alternative Approach — Using a Set (O(n log n))

An equally clean approach using `set()` instead of `dict.fromkeys()`:

```python
class Solution(object):
    def thirdMax(self, nums):
        unique = sorted(set(nums), reverse=True)
        return unique[2] if len(unique) >= 3 else unique[0]
```

Both approaches are functionally equivalent. The key difference is that `set()` does not preserve insertion order (which doesn't matter here since we sort anyway), while `dict.fromkeys()` does — making `dict.fromkeys()` the safer habit when order matters in other problems.
