# 66. Plus One

**Difficulty:** Easy  
**Topic Tags:** Array, Math  
**LeetCode Link:** [Plus One](https://leetcode.com/problems/plus-one/)

---

## Problem Description

You are given a **large integer** represented as an integer array `digits`, where each `digits[i]` is the `i`th digit of the integer. The digits are ordered from most significant to least significant (left to right), and there are no leading zeros.

Increment the large integer by one and return the resulting array of digits.

---

## Examples

**Example 1:**
```
Input:  digits = [1, 2, 3]
Output: [1, 2, 4]
Explanation: The array represents the integer 123. Incrementing by one gives 124.
```

**Example 2:**
```
Input:  digits = [4, 3, 2, 1]
Output: [4, 3, 2, 2]
Explanation: The array represents the integer 4321. Incrementing by one gives 4322.
```

**Example 3:**
```
Input:  digits = [9]
Output: [1, 0]
Explanation: The array represents the integer 9. Incrementing by one gives 10.
```

---

## Constraints

- `1 <= digits.length <= 100`
- `0 <= digits[i] <= 9`
- `digits` does not contain any leading zeros.

---

## Approach

**Traverse from the last digit backwards.**

The key insight is to handle carry propagation:
- If the current digit is less than `9`, simply increment it and return — no carry needed.
- If the current digit is `9`, set it to `0` and continue to the next digit (carry propagates).
- If all digits were `9` (e.g., `[9, 9, 9]`), prepend a `1` to the result (e.g., `[1, 0, 0, 0]`).

---

## Solution

```python
class Solution(object):
    def plusOne(self, digits):
        n = len(digits)

        # Traverse from the last digit backwards
        for i in range(n - 1, -1, -1):
            if digits[i] < 9:
                digits[i] += 1
                return digits
            digits[i] = 0  # since it was 9

        # If all digits were 9
        return [1] + digits
```

---

## Complexity Analysis

| | Complexity |
|---|---|
| **Time** | O(n) — at most one full traversal of the array |
| **Space** | O(1) — in-place modification (O(n) in the edge case of all 9s due to new array) |
