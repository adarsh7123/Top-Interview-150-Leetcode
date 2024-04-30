```markdown
# LeetCode Problem Solutions

## Problem 57: Insert Interval

**Difficulty:** Medium

**Topics:** Array, Sorting.

**Companies:** -

### Problem Description

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the ith interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

Note that you don't need to modify `intervals` in-place. You can make a new array and return it.

#### Example 1:

**Input:** 
```plaintext
intervals = [[1,3],[6,9]], newInterval = [2,5]
```
**Output:** 
```plaintext
[[1,5],[6,9]]
```

#### Example 2:

**Input:** 
```plaintext
intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
```
**Output:** 
```plaintext
[[1,2],[3,10],[12,16]]
```
**Explanation:** 
Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

**Constraints:**
- 0 <= intervals.length <= 10^4
- intervals[i].length == 2
- 0 <= starti <= endi <= 10^5
- `intervals` is sorted by `starti` in ascending order.
- `newInterval.length == 2`
- 0 <= start <= end <= 10^5

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals,
                               vector<int>& newInterval) {
        int n = intervals.size();
        vector<vector<int>> ans;
        int i =0;

        // Add intervals that end before newInterval starts.
        while(i<n && intervals[i][1]<newInterval[0]){
            ans.push_back(intervals[i]);
            i++;
        }

        // Merge intervals that overlap with newInterval.
        while(i<n && intervals[i][0]<=newInterval[1] ){
            newInterval[0]= min(intervals[i][0],newInterval[0]);
            newInterval[1]= max(intervals[i][1],newInterval[1]);
            i++;
        }
        ans.push_back(newInterval);

        // Add remaining intervals after newInterval.
        while(i<n){
            ans.push_back(intervals[i]);
            i++;
        }

    return ans;

    }
};
```
---
This solution inserts the new interval into the existing list of intervals while maintaining the sorted order and merging overlapping intervals.

---
