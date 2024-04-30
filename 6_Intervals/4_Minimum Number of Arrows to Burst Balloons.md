```markdown
# LeetCode Problem Solutions

## Problem 452: Minimum Number of Arrows to Burst Balloons

**Difficulty:** Medium

**Topics:** Greedy Algorithm, Sorting.

**Companies:** -

### Problem Description

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose horizontal diameter stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up directly vertically (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is burst by an arrow shot at x if `xstart <= x <= xend`. There is no limit to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return the minimum number of arrows that must be shot to burst all balloons.

#### Example 1:

**Input:** 
```plaintext
points = [[10,16],[2,8],[1,6],[7,12]]
```
**Output:** 
```plaintext
2
```
**Explanation:** 
The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].

#### Example 2:

**Input:** 
```plaintext
points = [[1,2],[3,4],[5,6],[7,8]]
```
**Output:** 
```plaintext
4
```
**Explanation:** 
One arrow needs to be shot for each balloon for a total of 4 arrows.

#### Example 3:

**Input:** 
```plaintext
points = [[1,2],[2,3],[3,4],[4,5]]
```
**Output:** 
```plaintext
2
```
**Explanation:** 
The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 2, bursting the balloons [1,2] and [2,3].
- Shoot an arrow at x = 4, bursting the balloons [3,4] and [4,5].

**Constraints:**
- 1 <= points.length <= 10^5
- points[i].length == 2
- -2^31 <= xstart < xend <= 2^31 - 1

### Solution

```cpp
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(),points.end());

        int y = points[0][1];

        int count =1;

        for (int i =1; i<points.size();i++){
            if(y<points[i][0]){
                count++;
                y= points[i][1];
            }

            y=min(points[i][1],y);
        }
        return count;
        
    }
};
```
---
This solution sorts the intervals by their starting points and then iterates through them, tracking the ending point of the current balloon. If the starting point of the next balloon is greater than the current ending point, a new arrow is required, and the ending point is updated accordingly.

---
```cpp
/*
 sort(points.begin(),points.end());
        int n = points.size();
        int cnt = 1;
        int mine = INT_MAX; 
        for(int i =0 ;i<n;i++)
        {
            int s = points[i][0];
            int e = points[i][1];
            if(s<=mine)
            {
                mine = min(e,mine);
            }
            else
            {
                mine = e;
                cnt++;
            }
        }
        return cnt;
        */
``` 
---
This is an alternative solution that achieves the same result using a different approach.

---
