```markdown
# LeetCode Problem Solutions

## Problem 228: Summary Ranges

**Difficulty:** Easy

**Topics:** Array, Two Pointers.

**Companies:** -

### Problem Description

You are given a sorted unique integer array nums.

A range [a,b] is the set of all integers from a to b (inclusive).

Return the smallest sorted list of ranges that cover all the numbers in the array exactly. That is, each element of nums is covered by exactly one of the ranges, and there is no integer x such that x is in one of the ranges but not in nums.

Each range [a,b] in the list should be output as:

"a->b" if a != b
"a" if a == b

#### Example 1:

**Input:** 
```plaintext
nums = [0,1,2,4,5,7]
```
**Output:** 
```plaintext
["0->2","4->5","7"]
```
**Explanation:** 
The ranges are:
- [0,2] --> "0->2"
- [4,5] --> "4->5"
- [7,7] --> "7"

#### Example 2:

**Input:** 
```plaintext
nums = [0,2,3,4,6,8,9]
```
**Output:** 
```plaintext
["0","2->4","6","8->9"]
```
**Explanation:** 
The ranges are:
- [0,0] --> "0"
- [2,4] --> "2->4"
- [6,6] --> "6"
- [8,9] --> "8->9"

**Constraints:**
- 0 <= nums.length <= 20
- -2^31 <= nums[i] <= 2^31 - 1
- All the values of nums are unique.
- nums is sorted in ascending order.

### Solution

```cpp
#include <vector>
#include <string>
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        vector<string> ans;
        // Check if the input vector is empty
        if (nums.empty())
            return ans;

        int start = nums[0];
        int end = start;

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] == end + 1) {
                end = nums[i];
            } else {
                
                if (start == end) {
                    ans.push_back(to_string(start));
                }else {
                    ans.push_back(to_string(start) + "->" + to_string(end));
                }
                start = end = nums[i];
            }
        }

        // add last range
        //  Single number start and end are same
        if (start == end) {
            ans.push_back(to_string(start));
        } else {
            ans.push_back(to_string(start) + "->" + to_string(end));
        }

        return ans;
    }
};
```
---
This solution iterates through the array, maintaining a start and end index for each range encountered. When a break in the sequence is found, it adds the range to the result vector. Finally, it adds the last range before returning the result.

---