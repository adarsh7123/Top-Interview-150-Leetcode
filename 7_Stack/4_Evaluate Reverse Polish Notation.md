```markdown
# LeetCode Problem Solutions

## Problem 150: Evaluate Reverse Polish Notation

**Difficulty:** Medium

**Topics:** Stack, Math.

**Companies:** -

### Problem Description

You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:
- The valid operators are '+', '-', '*', and '/'.
- Each operand may be an integer or another expression.
- The division between two integers always truncates toward zero.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a 32-bit integer.

#### Example 1:

**Input:** 
```plaintext
tokens = ["2","1","+","3","*"]
```
**Output:** 
```plaintext
9
```
**Explanation:** 
```plaintext
((2 + 1) * 3) = 9
```

**Constraints:**
- 1 <= tokens.length <= 10^4
- tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

### Solution

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        int i = 0;
        while (i < tokens.size()) {
            if (tokens[i] != "+" && tokens[i] != "-" && tokens[i] != "*" && tokens[i] != "/") {
                    st.push(stoi(tokens[i]));
            }
            else{
                int a = st.top(); st.pop();
                int b = st.top(); st.pop();
                if(tokens[i]=="+") st.push(b+a);
                else if(tokens[i]=="-") st.push(b-a);
                else if(tokens[i]=="*") st.push(b*a);
                else if(tokens[i]=="/") st.push(b/a);

            }
            i++;

        }

        return st.top();
    }
};
```
---