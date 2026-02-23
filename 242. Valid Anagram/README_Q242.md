# 242. Valid Anagram

**Difficulty:** Easy  
**Topic Tags:** Hash Table, String, Sorting  
**LeetCode Link:** [https://leetcode.com/problems/valid-anagram/](https://leetcode.com/problems/valid-anagram/)

---

## Problem Description

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### Examples

**Example 1:**
```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**
```
Input: s = "rat", t = "car"
Output: false
```

### Constraints

- `1 <= s.length, t.length <= 5 * 10⁴`
- `s` and `t` consist of lowercase English letters.

---

## Approach — Sorting

If two strings are anagrams of each other, they must contain the **exact same characters in the same quantities**. Sorting both strings alphabetically will produce identical results if and only if they are anagrams.

### Key Observations

- If `s` and `t` have different lengths, they cannot be anagrams — `sorted()` handles this implicitly since the sorted arrays would differ in size.
- Sorting reduces the problem to a simple equality check: if `sorted(s) == sorted(t)`, the strings are anagrams.
- This is one of the most readable and concise approaches to the problem.

### Complexity

| | Complexity |
|---|---|
| **Time** | O(n log n) — dominated by the sorting step |
| **Space** | O(n) — sorted() creates a new list of characters |

---

## Solution

```python
class Solution(object):
    def isAnagram(self, s, t):
        if sorted(s) == sorted(t):
            return True
        else:
            return False
```

---

## Walkthrough

**Example 1:** `s = "anagram"`, `t = "nagaram"`

```
sorted("anagram") → ['a', 'a', 'a', 'g', 'm', 'n', 'r']
sorted("nagaram") → ['a', 'a', 'a', 'g', 'm', 'n', 'r']

['a', 'a', 'a', 'g', 'm', 'n', 'r'] == ['a', 'a', 'a', 'g', 'm', 'n', 'r'] ✅
```
✅ Output: `true`

---

**Example 2:** `s = "rat"`, `t = "car"`

```
sorted("rat") → ['a', 'r', 't']
sorted("car") → ['a', 'c', 'r']

['a', 'r', 't'] == ['a', 'c', 'r'] ❌
```
✅ Output: `false`

---

## Alternative Approach — Hash Map (O(n))

For a more optimal solution, a **character frequency counter** can be used instead of sorting, reducing time complexity to O(n):

```python
from collections import Counter

class Solution(object):
    def isAnagram(self, s, t):
        return Counter(s) == Counter(t)
```

`Counter` builds a frequency map of each character and compares them directly, avoiding the overhead of sorting entirely.
