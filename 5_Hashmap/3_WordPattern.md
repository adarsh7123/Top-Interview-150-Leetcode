```markdown
# LeetCode Problem Solutions

## Problem 290: Word Pattern

**Difficulty:** Easy

**Topics:** Hash Table, String.

**Companies:** -

### Problem Description

Given a pattern and a string `s`, find if `s` follows the same pattern.

Here "follow" means a full match, such that there is a bijection between a letter in pattern and a non-empty word in `s`.

#### Example 1:

**Input:** 
```plaintext
pattern = "abba", s = "dog cat cat dog"
```
**Output:** 
```plaintext
true
```

#### Example 2:

**Input:** 
```plaintext
pattern = "abba", s = "dog cat cat fish"
```
**Output:** 
```plaintext
false
```

**Constraints:**
- 1 <= pattern.length <= 300
- `pattern` contains only lower-case English letters.
- 1 <= s.length <= 3000
- `s` contains only lowercase English letters and spaces ' '.
- `s` does not contain any leading or trailing spaces.
- All the words in `s` are separated by a single space.

### Solution

```cpp
class Solution {
public:
    bool wordPattern(string pattern, string s) {
        unordered_map<char, string> charToWord; // Map each character in pattern to a word in s
        unordered_map<string, char> wordToChar; // Map each word in s to a character in pattern
        
        int i = 0; // Index for traversing the string s
        stringstream ss(s); // Use stringstream to split the string s into words
        
        for (char c : pattern) {
            string word;
            if (!(ss >> word)) return false; // If no more words in s, return false
            
            // Check if the current character in pattern has already been mapped to a different word
            if (charToWord.find(c) != charToWord.end() && charToWord[c] != word) return false;
            
            // Check if the current word in s has already been mapped to a different character
            if (wordToChar.find(word) != wordToChar.end() && wordToChar[word] != c) return false;
            
            // Map the current character to the current word
            charToWord[c] = word;
            // Map the current word to the current character
            wordToChar[word] = c;
        }
        
        // If there are more words in s than characters in pattern, return false
        string word;
        if (ss >> word) return false;
        
        return true; // If all checks pass, return true
    }
};
```
---
This solution uses two unordered maps to map each character in the pattern to a word in `s` and vice versa. It iterates through the pattern and the string `s` simultaneously and checks if the mappings are consistent. If they are inconsistent, it returns false. Otherwise, it returns true.

---