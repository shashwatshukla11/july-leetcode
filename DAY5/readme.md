# 📅 Day 5 – Find Lucky Integer in an Array

#### 🔗 LeetCode Problem: [1394. Find Lucky Integer in an Array](https://leetcode.com/problems/find-lucky-integer-in-an-array/)  
#### 💡 Difficulty: Easy  
#### 🧠 Topic Tags: Array, Hash Table, Counting

---

## ✍️ Problem Summary

Given an array of integers `arr`, a **lucky integer** is an integer that has a **frequency in the array equal to its value**.

Return the **largest lucky integer** in the array.  
If there is **no lucky integer**, return `-1`.

---

## 🔍 Examples

### Example 1
**Input:** `[2, 2, 3, 4]`  
**Output:** `2`  
**Explanation:** The only lucky number is `2` as it appears exactly 2 times.

---

### Example 2
**Input:** `[1, 2, 2, 3, 3, 3]`  
**Output:** `3`  
**Explanation:** All of 1, 2, and 3 are lucky numbers, return the largest one.

---

### Example 3
**Input:** `[2, 2, 2, 3, 3]`  
**Output:** `-1`  
**Explanation:** No integer appears exactly as many times as its value.

---

## 🚧 My Approach

- Use a **frequency array** of size 501 (since `1 <= arr[i] <= 500`).
- Count how many times each number appears in the input array.
- Loop through the frequency array and **check if frequency matches the number itself**.
- Track and return the **largest such lucky number**, or return `-1` if none exists.

---

## ✅ Java Solution

```java
class Solution {
    public int findLucky(int[] arr) {
        int[] freq = new int[501]; // Frequency array

        for (int num : arr) {
            freq[num]++;
        }

        int ans = -1;
        for (int i = 1; i <= 500; i++) {
            if (freq[i] == i) {
                ans = i; // Update if a lucky number is found
            }
        }

        return ans;
    }
}
