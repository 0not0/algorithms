# [940. Distinct Subsequences II](https://leetcode.com/problems/distinct-subsequences-ii/)  

`Hard` level  

<br />

***

### Solution

**Time complexity:**  <code>O(n * m)</code>  
**Space complexity:**  <code>O(m)</code>  

**C++**

```C++
class Solution {
public:
  int distinctSubseqII(string s) {
    const int MOD = 1e9 + 7;

    long long dp = 1;
    long long last[26] = {};

    for(char c : s)
    {
      int index = c - 'a';
      long long prevDp = dp;

      dp = (2 * dp - last[index] + MOD) % MOD;

      last[index] = prevDp;
    }

    return (dp - 1 + MOD) % MOD;
  }
};
```