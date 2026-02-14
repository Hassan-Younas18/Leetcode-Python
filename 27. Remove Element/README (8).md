# 20. Valid Parentheses

## Problem Description

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

## Examples

### Example 1:
```
Input: s = "()"
Output: true
```

### Example 2:
```
Input: s = "()[]{}"
Output: true
```

### Example 3:
```
Input: s = "(]"
Output: false
```

### Example 4:
```
Input: s = "([])"
Output: true
```

## Constraints

- `1 <= s.length <= 10^4`
- `s` consists of parentheses only `'()[]{}'`

## Approach

This problem is best solved using a **stack** data structure. The key insight is:
- When we encounter an opening bracket, push it onto the stack
- When we encounter a closing bracket, check if it matches the most recent opening bracket (top of stack)
- If all brackets are properly matched, the stack should be empty at the end

### Algorithm:
1. Create an empty stack
2. Iterate through each character in the string:
   - If it's an opening bracket `(`, `{`, or `[`, push it onto the stack
   - If it's a closing bracket `)`, `}`, or `]`:
     - Check if the stack is empty (no matching opening bracket) → return false
     - Pop from the stack and verify it matches the closing bracket
     - If it doesn't match → return false
3. After iterating, check if the stack is empty
   - Empty stack → all brackets matched → return true
   - Non-empty stack → unmatched opening brackets → return false

## Complexity Analysis

- **Time Complexity:** O(n), where n is the length of the string. We traverse the string once.
- **Space Complexity:** O(n) in the worst case, when all characters are opening brackets and get pushed onto the stack.

## Key Insights

- Stack is ideal for problems involving nested structures or matching pairs
- The LIFO (Last In First Out) property of stacks naturally handles the "most recent unmatched bracket" logic
- Edge cases to consider: empty string, only opening brackets, only closing brackets, mismatched pairs

## Tags

`Stack` `String` `Easy`

## Related Problems

- LeetCode 22: Generate Parentheses
- LeetCode 32: Longest Valid Parentheses
- LeetCode 301: Remove Invalid Parentheses
