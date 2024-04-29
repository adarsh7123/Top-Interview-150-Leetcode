

---

# Ransom Note

## Problem Description

Given two strings `ransomNote` and `magazine`, return true if `ransomNote` can be constructed by using the letters from `magazine` and false otherwise. Each letter in `magazine` can only be used once in `ransomNote`.

## Examples

**Example 1:**

Input:
```
ransomNote = "a"
magazine = "b"
```

Output:
```
false
```

**Example 2:**

Input:
```
ransomNote = "aa"
magazine = "ab"
```

Output:
```
false
```

**Example 3:**

Input:
```
ransomNote = "aa"
magazine = "aab"
```

Output:
```
true
```

## Constraints

- `1 <= ransomNote.length, magazine.length <= 10^5`
- `ransomNote` and `magazine` consist of lowercase English letters.

## Algorithm

The solution checks if each character in the `ransomNote` string appears in the `magazine` string. It uses a hashmap to store the frequency of characters in the `magazine` string. Then, it iterates through the `ransomNote` string and checks if each character is present in the hashmap and if its frequency is greater than 0. If so, it decrements the frequency in the hashmap. If not, it returns false. If the loop completes without returning false, it returns true.

## Code Implementation

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        // base case
        if (ransomNote.size() > magazine.size())
            return false;

        // hash
        unordered_map<char, int> dictionary;

        // add all letter occurence of magazine in dictionary
        for (char c : magazine) {
            if (dictionary.find(c) == dictionary.end()) {
                dictionary[c] = 1;
            } else {
                dictionary[c]++;
            }
        }

        // compare ransomNote letter with dictionary
        for (char c : ransomNote) {
            if (dictionary.find(c) != dictionary.end() && dictionary[c] > 0) {
                dictionary[c]--;
            } else {
                return false;
            }
        }
        return true;
    }
};
```

## Optimal Implementation

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        unordered_map<char, int> freq;
        for (char c : magazine) {
            freq[c]++;
        }
        for (char c : ransomNote) {
            if (freq.find(c) == freq.end() || freq[c] == 0) {
                return false;
            }
            freq[c]--;
        }
        return true;
    }
};
```
---
