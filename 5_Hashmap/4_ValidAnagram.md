```markdown
# LeetCode Problem Solutions

## Problem 242: Valid Anagram

**Difficulty:** Easy

**Topics:** Hash Table, Sorting.

**Companies:** -

### Problem Description

Given two strings `s` and `t`, return true if `t` is an anagram of `s`, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

#### Example 1:

**Input:** 
```plaintext
s = "anagram", t = "nagaram"
```
**Output:** 
```plaintext
true
```

#### Example 2:

**Input:** 
```plaintext
s = "rat", t = "car"
```
**Output:** 
```plaintext
false
```

**Constraints:**
- 1 <= s.length, t.length <= 5 * 10^4
- `s` and `t` consist of lowercase English letters.

**Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

### Solution

```cpp
#include <bits/stdc++.h>
class Solution {
public:
    bool isAnagram(string s, string t) {
        /*
         unordered_map<char, int> count;
        if (s.size() != t.size())
            return false;

        for (char c : s) {
            if (count.find(c) == count.end()) {
                count[c] = 1;
            }else{
            count[c]++;
            }
        }

        for(char c : t){
            if(count.find(c)!=count.end() && count[c]>0){
                count[c]--;
            }
            else{
                return false;
            }
        }

        return true;
    }*/
    
        /* if (s.size() != t.size())
             return false;

         unordered_map<char, int> count;

         for (char c : s) {

             count[c]++;
         }

         for (char c : t) {
             if (--count[c] < 0)
                 return false;
         }

         return true;*/

        if (s.size() != t.size())
            return false;

        vector<int> count(27, 0);

        for (char c : s) {
            count[c - 'a'] += 1;
        }
        for (char c : t) {
            count[c - 'a'] -= 1;
        }

        for (int i = 0; i <= 26; i++) {
            if (count[i] != 0)
                return false;
        }
        return true;
    }
};
```

---
This solution provides three different implementations for checking if two strings are anagrams of each other. The first implementation uses an unordered map to count the frequency of characters in both strings. The second implementation uses a similar approach but with a vector instead of an unordered map. The third implementation is the most optimized one, using only a vector to count the frequency of characters.

---