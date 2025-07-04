# 📅 LeetCode Daily Challenge – Day 2


### 🔗 LeetCode Problem: [3307. Find the K-th Character in String Game II](https://leetcode.com/problems/find-the-k-th-character-in-string-game-ii/)
### 💡 Difficulty: Hard  
### 🧠 Topic Tags: Simulation, Binary Search, Bit Manipulation, String Construction  


## ✍️ Problem Summary  
Alice and Bob are playing a game. Initially, `word = "a"`.  
You are given:  
- A **positive integer** `k`  
- An integer **array** `operations`, where:  
  - `0` → Append a **copy** of the current word to itself  
  - `1` → Append a **shifted** version (next character of each letter) to the current word (e.g., `"zb"` → `"zbac"`)  

After all operations, return the `k`-th character in the final word. The final string is **guaranteed to have at least `k` characters**.


## 📌 Example  

### Example 1  
**Input**:  
`k = 5`  
`operations = [0, 0, 0]`  

**Output**:  
`"a"`  

**Explanation**:  
- Start: `"a"`  
- After 1st op: `"a" + "a"` → `"aa"`  
- After 2nd op: `"aa" + "aa"` → `"aaaa"`  
- After 3rd op: `"aaaa" + "aaaa"` → `"aaaaaaaa"`  
- 5th character = `'a'`



### Example 2  
**Input**:  
`k = 10`  
`operations = [0, 1, 0, 1]`  

**Output**:  
`"b"`  

**Explanation**:  
- `"a"` → `"aa"`  
- `"aa" + bb"` → `"aabb"`  
- `"aabb + aabb"` → `"aabbaabb"`  
- `"aabbaabb + bbccbbcc"` → `"aabbaabbbbccbbcc"`  
- 10th character = `'b'`


## 🚧 My Approach  
We **don’t build the whole string** — that would be infeasible with `k` up to `10¹⁴`.

### Key Insight:
- The final string is a result of recursive doubling and character shifting.
- Track **how many shifts** were applied to reach the `k`-th character by **reversing the operations**.
- Precompute the **length after each operation** using powers of 2 (like a prefix doubling sequence).
- Walk backwards from the final `k`, adjusting it to refer to the first or second half (depending on the op), and count how many shifts happened.

## ✅ Java Code  
```java
class Solution {
    public char kthCharacter(long k, int[] operations) {
        if (k == 1) return 'a';
        
        int cnt = 0;
        int n = operations.length;
        long[] pow2 = new long[n + 1];
        pow2[0] = 1;
        
        // Precompute length after each operation
        for (int i = 1; i <= n; i++) {
            long doubled = pow2[i - 1] << 1;
            pow2[i] = doubled > 0 ? doubled : Long.MAX_VALUE;
        }
        
        // Trace back from k to original character
        while (k > 1) {
            int i = 1;
            while (i <= n && pow2[i] < k) i++;
            
            k -= pow2[i - 1]; // Move to second half
            if (operations[i - 1] == 1) cnt++; // If it was shifted, record that
        }
        
        return (char)('a' + cnt % 26); // Apply shift to 'a'
    }
}
```

---

Let me know if you want this in `.md` file format or want to continue with Day 3 🚀
