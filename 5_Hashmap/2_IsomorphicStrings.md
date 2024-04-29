Certainly! Here's the Markdown file with both the original solution and the additional optimal solution added:

```markdown
# LeetCode Problem Solutions

## Problem 205: Isomorphic Strings

**Difficulty:** Easy

**Topics:** Hash Table, Two Pointers, String.

**Companies:** -

### Problem Description

Given two strings `s` and `t`, determine if they are isomorphic.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

#### Example 1:

**Input:** 
```plaintext
s = "egg", t = "add"
```

**Output:** 
```plaintext
true
```

#### Example 2:

**Input:** 
```plaintext
s = "foo", t = "bar"
```

**Output:** 
```plaintext
false
```

#### Example 3:

**Input:** 
```plaintext
s = "paper", t = "title"
```

**Output:** 
```plaintext
true
```

**Constraints:**
- 1 <= s.length <= 5 * 10^4
- t.length == s.length
- `s` and `t` consist of any valid ASCII character.

### Original Solution

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if (s.size() != t.size())
            return false;

        vector<int> indexS(200, 0);
        vector<int> indexT(200, 0);

        for (int i = 0; i < s.size(); i++) {
            if (indexS[s[i]] != indexT[t[i]]) {
                return false;
            }
            indexS[s[i]] = i + 1;
            indexT[t[i]] = i + 1;
        }

        return true;
    }
};
```

### Additional Optimal Solution

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char, char> s_to_t, t_to_s;
        
        for (int i = 0; i < s.size(); ++i) {
            if (s_to_t.find(s[i]) == s_to_t.end() && t_to_s.find(t[i]) == t_to_s.end()) {
                s_to_t[s[i]] = t[i];
                t_to_s[t[i]] = s[i];
            } else {
                if (s_to_t[s[i]] != t[i] || t_to_s[t[i]] != s[i]) {
                    return false;
                }
            }
        }
        
        return true;
    }
};
```
---

This additional optimal solution uses unordered maps `s_to_t` and `t_to_s` to map characters from `s` to `t` and vice versa. It iterates through both strings simultaneously and checks if the mappings are consistent. If they are inconsistent, it returns false. Otherwise, it returns true.
---