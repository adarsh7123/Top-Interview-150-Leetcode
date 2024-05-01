```markdown
# LeetCode Problem Solutions

## Problem 224: Basic Calculator

**Difficulty:** Hard

**Topics:** Stack, Math.

**Companies:** -

### Problem Description

Given a string s representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

Note: You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as eval().

#### Example 1:

**Input:** 
```plaintext
s = "1 + 1"
```
**Output:** 
```plaintext
2
```

**Constraints:**
- 1 <= s.length <= 3 * 10^5
- s consists of digits, '+', '-', '(', ')', and ' '.
- s represents a valid expression.
- '+' is not used as a unary operation (i.e., "+1" and "+(2 + 3)" is invalid).
- '-' could be used as a unary operation (i.e., "-1" and "-(2 + 3)" is valid).
- There will be no two consecutive operators in the input.
- Every number and running calculation will fit in a signed 32-bit integer.

### Solution

```cpp
class Solution {
public:
    int calculate(string s) {
        stack<pair<int, int>> st;

        // first intilaize two vars , sum and sign
        // sum = 0
        long long int sum = 0;
        // sign = +1
        int sign = +1;

        // traverse the string:
        for (int i = 0; i < s.size(); ++i) {
            char ch = s[i];
            //     if(ch is digit)
            if (isdigit(ch)) {
                // num = get_full_num; // may be multidigit
                long long int num = 0;
                while (i < s.size() && isdigit(s[i])) {
                    //  add it to sum , sum += (num * sign)
                    num = (num * 10) + s[i] - '0';
                    i++;
                }
                i--;
                sum += (num * sign);
                //  reset sign to +1
                sign = +1;
            }
            //     else if(ch is '(')
            else if (ch == '(') {
                //         save current state of sum and sign in stack
                st.push(make_pair(sum, sign));
                //         reset sum and sign
                sum = 0;
                sign = +1;
            }
            //     else if(ch is ')')
            else if (ch == ')') {
                //         sum = val_at_top + (sign_at_top * sum)
                sum = st.top().first + (st.top().second * sum);
                st.pop();
                //         pop;
            }
            //     else if(ch is '-')
            else if (ch == '-') {
                //         toggle sign
                sign = (-1 * sign);
            }
        }
        return sum;
    }
};
```
---