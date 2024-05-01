```markdown
# LeetCode Problem Solutions

## Problem 20: Valid Parentheses

**Difficulty:** Easy

**Topics:** Stack, String.

**Companies:** -

### Problem Description

Given a string `s` containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.

#### Example 1:

**Input:** 
```plaintext
s = "()"
```
**Output:** 
```plaintext
true
```

#### Example 2:

**Input:** 
```plaintext
s = "()[]{}"
```
**Output:** 
```plaintext
true
```

#### Example 3:

**Input:** 
```plaintext
s = "(]"
```
**Output:** 
```plaintext
false
```

**Constraints:**
- 1 <= s.length <= 10^4
- s consists of parentheses only '()[]{}'.

### Solution

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[') {
                st.push(c);
            } else {
                 if (st.empty() || 
                    (c == ')' && st.top() != '(') || 
                    (c == '}' && st.top() != '{') ||
                    (c == ']' && st.top() != '[')){
                    return false;
                }
                st.pop();
            }
        }

        return st.empty();
    }
};
```
---

This solution uses a stack to keep track of opening brackets. It iterates through the input string, pushing opening brackets onto the stack and popping them when encountering a closing bracket. If the stack is empty when encountering a closing bracket or if the closing bracket does not match the corresponding opening bracket, it returns false. Otherwise, it returns true if the stack is empty at the end of iteration.

---