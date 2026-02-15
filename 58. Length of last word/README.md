# 58. Length of Last Word

## Problem Description

Given a string `s` consisting of words and spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

## Examples

**Example 1:**
```
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

**Example 2:**
```
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

**Example 3:**
```
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

## Constraints

- 1 <= s.length <= 10⁴
- `s` consists of only English letters and spaces ' '
- There will be at least one word in `s`

## Solution

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        word="Hello world"
        for i in s.split():
            length=len(i)
        return length   
```

## Approach

The solution uses Python's built-in `split()` method to break the string into words:

1. **Split the string**: `s.split()` divides the string by whitespace and returns a list of words
2. **Iterate through words**: Loop through each word in the list
3. **Track length**: Store the length of each word
4. **Return last length**: After the loop completes, the length variable contains the length of the last word

## Complexity Analysis

- **Time Complexity**: O(n), where n is the length of the string. We iterate through the string once during the split operation.
- **Space Complexity**: O(n), for storing the split words in a list.

## Alternative Approach

A more space-efficient solution would be to iterate from the end of the string:

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        s = s.strip()  # Remove trailing spaces
        return len(s.split()[-1])
```

This directly accesses the last word without iterating through all words.

## LeetCode Link

[Problem 58 - Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

## Difficulty

Easy

## Tags

- String
- Array
