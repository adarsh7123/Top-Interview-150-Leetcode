```markdown
# LeetCode Problem Solutions

## Problem 155: Min Stack

**Difficulty:** Medium

**Topics:** Stack, Design.

**Companies:** -

### Problem Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element val onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with O(1) time complexity for each function.

#### Example 1:

**Input:**
```plaintext
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
```
**Output:** 
```plaintext
[null,null,null,null,-3,null,0,-2]
```
**Explanation:**
```plaintext
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```

**Constraints:**
- -2^31 <= val <= 2^31 - 1
- Methods pop, top and getMin operations will always be called on non-empty stacks.
- At most 3 * 10^4 calls will be made to push, pop, top, and getMin.

### Solution

```cpp
class MinStack {
public:
    vector<pair<int,int>> s;
    MinStack() {
        
    }
    
    void push(int val) {
        if(s.empty()){
            s.push_back({val,val});
        }
        else{
            s.push_back({val, min(s.back().second , val)});
        }
    }
    
    void pop() {
        s.pop_back();
    }
    
    int top() {
        return s.back().first;
    }
    
    int getMin() {
        return s.back().second;
    }
};
```

This solution uses a vector of pairs to store both the elements and the minimum element seen so far. The `push`, `pop`, `top`, and `getMin` operations are all implemented with O(1) time complexity.

```cpp
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```
---
