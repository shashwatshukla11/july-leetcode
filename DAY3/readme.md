# 📅 LeetCode Daily Challenge – Day 3

### 🔗 LeetCode Problem: [3304. Find the K-th Character in String Game I](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/)  
### 💡 Difficulty: Easy  
### 🧠 Topic Tags: Bit Manipulation, String Simulation  

## ✍️ Problem Summary  
Alice starts with the string `"a"` and repeatedly appends a version of the current string where every character is shifted to its next character in the English alphabet (wrapping around from `'z'` to `'a'`).  

You are given a positive integer `k`. Return the `k`-th character of the string after enough operations are performed to make the length at least `k`.
## 📌 Example  
**Input**: `k = 5`  
**Output**: `"b"`  

**Explanation**:  
- Initial word = `"a"`  
- 1st operation → `"a"` + `"b"` → `"ab"`  
- 2nd operation → `"ab"` + `"bc"` → `"abbc"`  
- 3rd operation → `"abbc"` + `"bccd"` → `"abbcbccd"`  
- The 5th character is `'b'`

## 🚧 My Approach  
We don’t need to simulate the full string. Instead:  
- Think of `k - 1` in binary.  
- The number of **1s** (i.e. `bitCount(k - 1)`) tells how many times the character at that position has been shifted.  
- So the answer is `'a' + bitcount(k - 1)`.

## ✅ Java Code  
```java
class Solution {
    public char kthCharacter(int k) {
        return (char) ('a' + Integer.bitCount(k - 1));
    }
}
```
