
---

## 125. Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return true if it is a palindrome, or false otherwise.

### Example 1:

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

### Example 2:

```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

### Example 3:

```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

### Constraints:

- 1 <= s.length <= 2 * 10^5
- `s` consists only of printable ASCII characters.

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int start = 0, end = s.size() - 1;
        if (s.size() == 0)
            return true;

        while (start < end) {
            if (!isalnum(s[start])) {
                start++;
                continue;
            } else if (!isalnum(s[end])) {
                end--;
                continue;
            } else {
                if (tolower(s[start]) != tolower(s[end])) {
                    return false;
                } else {
                    start++, end--;
                }
            }
        }
        return true;
    }
};

/*
bool isPalindrome(string s) {
    string check;
    int a = s.size();
    if (a == 0) return true;
    for (int i = 0; i < a; i++) {
        // Check if the character is alphanumeric
        if ((s[i] >= '0' && s[i] <= '9') || (s[i] >= 'a' && s[i] <= 'z')) {
            check += s[i];
        } else if (s[i] >= 'A' && s[i] <= 'Z') {
            // Convert uppercase letters to lowercase
            check += (s[i] - 'A') + 'a';
        }
    }

    // Now, check if the processed string is a palindrome
    // Iterate over the range [0, N/2]
    for (int i = 0; i < check.length() / 2; i++) {
        // If check[i] is not equal to the check[N-i-1]
        if (check[i] != check[check.length() - i - 1]) {
            // Return No
            return false;
        }
    }
    // Return "Yes"
    return true;
}
*/
```

---
