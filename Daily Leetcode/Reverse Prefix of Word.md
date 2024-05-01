```markdown
# LeetCode Problem Solutions

## Problem 2000: Reverse Prefix of Word

**Difficulty:** Easy

**Topics:** String.

**Companies:** -

### Problem Description

Given a 0-indexed string word and a character ch, reverse the segment of word that starts at index 0 and ends at the index of the first occurrence of ch (inclusive). If the character ch does not exist in word, do nothing.

Return the resulting string.

#### Example 1:

**Input:** 
```plaintext
word = "abcdefd", ch = "d"
```
**Output:** 
```plaintext
"dcbaefd"
```
**Explanation:** 
The first occurrence of "d" is at index 3. 
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "dcbaefd".

#### Example 2:

**Input:** 
```plaintext
word = "xyxzxe", ch = "z"
```
**Output:** 
```plaintext
"zxyxxe"
```
**Explanation:** 
The first and only occurrence of "z" is at index 3.
Reverse the part of word from 0 to 3 (inclusive), the resulting string is "zxyxxe".

#### Example 3:

**Input:** 
```plaintext
word = "abcd", ch = "z"
```
**Output:** 
```plaintext
"abcd"
```
**Explanation:** 
"z" does not exist in word.
You should not do any reverse operation, the resulting string is "abcd".

**Constraints:**
- 1 <= word.length <= 250
- word consists of lowercase English letters.
- ch is a lowercase English letter.

### Solutions

#### Approach 1:

```cpp
class Solution {
public:
    string reversePrefix(string word, char ch) {
        int i = 0, j = 0;
        while (j < word.size() && word[j] != ch)
            j++;
        if (word[j] != ch)
            return word;
        while (i <= j)
            swap(word[i++], word[j--]);
        return word;
    }
};
```

#### Approach 2:

```cpp
class Solution {
public:
    string reversePrefix(string word, char ch) {
        int j = word.find(ch);

        if(j!=-1){
            reverse(word.begin(),word.begin()+j+1);
        }
        return word;
    }
};
```
---