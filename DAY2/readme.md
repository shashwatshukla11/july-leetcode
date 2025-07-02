## 📅 LeetCode Daily Challenge – Day 2
### 🔗 LeetCode Problem: [3333. Find the Original Typed String II](https://leetcode.com/problems/find-the-original-typed-string-ii)  
### 💡 Difficulty: Hard  
### 🧠 Topic Tags: DP, Combinatorics, Strings, Prefix Sum  

---

### ✍️ Problem Summary  
Alice types on her keyboard but may press a key for too long, resulting in repeated characters. Given a final output string `word` and a number `k`, return the number of original strings Alice might have intended to type such that the length of the original string is **at least `k`**. Return the result modulo `10⁹ + 7`.

---

### 🚧 My Approach  
- Group consecutive repeating characters into counts.  
  Example: `"aabbccdd"` → `[2, 2, 2, 2]`
- The number of ways to type each group is equal to its size (`g[i]` options: 1 to `g[i]` characters).
- The **total combinations** = product of all group sizes.
- We subtract invalid combinations (i.e., those with original length < `k`) using DP.

---

### ✅ Java Code

```java
public class Solution {
    private static final int MOD = (int)1e9 + 7;

    public int possibleStringCount(String word, int k) {
        if (word.isEmpty()) return 0;

        List<Integer> groups = new ArrayList<>();
        int count = 1;
        for (int i = 1; i < word.length(); i++) {
            if (word.charAt(i) == word.charAt(i - 1)) count++;
            else {
                groups.add(count);
                count = 1;
            }
        }
        groups.add(count);

        long total = 1;
        for (int num : groups) total = (total * num) % MOD;

        if (k <= groups.size()) return (int)total;

        int[] dp = new int[k];
        dp[0] = 1;
        for (int num : groups) {
            int[] newDp = new int[k];
            long sum = 0;
            for (int s = 0; s < k; s++) {
                if (s > 0) sum = (sum + dp[s - 1]) % MOD;
                if (s > num) sum = (sum - dp[s - num - 1] + MOD) % MOD;
                newDp[s] = (int)sum;
            }
            dp = newDp;
        }
        long invalid = 0;
        for (int s = groups.size(); s < k; s++) invalid = (invalid + dp[s]) % MOD;

        return (int)((total - invalid + MOD) % MOD);
    }
}
