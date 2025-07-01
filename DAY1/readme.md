# 📅 Day 1 – Find the Original Typed String I

#### 🔗 LeetCode Problem: [3330. Find the Original Typed String I](https://leetcode.com/problems/find-the-original-typed-string-i/)  
#### 💡 Difficulty: Easy  
#### 🧠 Topic Tags: String, Counting, Two Pointers

---

## ✍️ Problem Summary

Alice is typing a string but may press a key for too long, causing one character to repeat multiple times.  
This could happen **at most once** throughout the entire string.

You're given the final typed string. Return the **total number of possible original strings** Alice might have meant to type.

---

## 🔍 Examples

### Example 1
**Input:** `"abbcccc"`  
**Output:** `5`  
**Explanation:**

The possible original strings are:
- "abbcccc"
- "abbccc"
- "abbcc"
- "abbc"
- "abcccc"

---

### Example 2
**Input:** `"abcd"`  
**Output:** `1`

---

### Example 3
**Input:** `"aaaa"`  
**Output:** `4`

---

## 🚧 My Approach

- Traverse the string and **group consecutive characters** using two pointers.
- For each group of repeated characters:
  - If the group length is `k`, Alice may have intended any length from `1` to `k`.
  - But since Alice made this typing mistake **at most once**, we can apply this shortening to only one group.
- So, for each group of length `>1`, we count `(k - 1)` **extra possibilities**.
- Total possibilities = `1 (no mistake)` + `sum of (groupLen - 1)` for each group with length > 1.

---

## ✅ Java Solution

```java
class Solution {
    public int possibleStringCount(String word) {
        int n = word.length();
        int result = 1;  // base case: no shortening
        int i = 0;

        while (i < n) {
            int j = i;
            while (j < n && word.charAt(j) == word.charAt(i)) {
                j++;
            }
            int groupLen = j - i;
            if (groupLen > 1) {
                result += (groupLen - 1);
            }
            i = j;
        }

        return result;
    }
}
