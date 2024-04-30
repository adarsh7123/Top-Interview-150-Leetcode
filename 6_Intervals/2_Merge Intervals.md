```markdown
# LeetCode Problem Solutions

## Problem 56: Merge Intervals

**Difficulty:** Medium

**Topics:** Array, Sorting.

**Companies:** -

### Problem Description

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

#### Example 1:

**Input:** 
```plaintext
intervals = [[1,3],[2,6],[8,10],[15,18]]
```
**Output:** 
```plaintext
[[1,6],[8,10],[15,18]]
```
**Explanation:** 
Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

#### Example 2:

**Input:** 
```plaintext
intervals = [[1,4],[4,5]]
```
**Output:** 
```plaintext
[[1,5]]
```
**Explanation:** 
Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**
- 1 <= intervals.length <= 10^4
- intervals[i].length == 2
- 0 <= starti <= endi <= 10^4

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int n = intervals.size();
        if (n <= 1)
            return intervals;
        
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        ans.push_back(intervals[0]); // put 1st interval

        int i = 1;
        while (i < n) {
            if (intervals[i][0] <= ans.back()[1]) {
                ans.back()[1] = max(ans.back()[1], intervals[i][1]);
            } else {
                ans.push_back(intervals[i]);
            }
            i++;
        }

        return ans;
    }
};
```
---
This solution sorts the intervals based on their start times and then iterates through them to merge overlapping intervals into a single interval.

---
