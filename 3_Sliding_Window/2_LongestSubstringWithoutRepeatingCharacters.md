
---

## 3. Longest Substring Without Repeating Characters

Given a string `s`, find the length of the longest substring without repeating characters.

### Example 1:

**Input:**
```
s = "abcabcbb"
```

**Output:**
```
3
```

**Explanation:**
The answer is "abc", with the length of 3.

### Example 2:

**Input:**
```
s = "bbbbb"
```

**Output:**
```
1
```

**Explanation:**
The answer is "b", with the length of 1.

### Example 3:

**Input:**
```
s = "pwwkew"
```

**Output:**
```
3
```

**Explanation:**
The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

### Constraints:

- `0 <= s.length <= 5 * 10^4`
- `s` consists of English letters, digits, symbols, and spaces.

### Solution:

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if (n == 0 || n == 1) {
            return n;
        }

        vector<int> index(256, -1);
     
        int ans = 0;
        int start = -1;

        for (int i = 0; i < n; i++) {
            if (index[s[i]] > start) {
                start = index[s[i]];
            }

            index[s[i]] = i;
            
            ans = max(ans, i - start);
        }
        return ans;
    }
};
```

---
