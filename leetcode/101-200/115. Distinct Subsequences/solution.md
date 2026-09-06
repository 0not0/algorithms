# [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

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
  int numDistinct(string s, string t) {
    int m = t.size();

    vector<unsigned long long> dp(m + 1, 0);
    dp[0] = 1;

    for(char c : s)
    {
      for(int j = m; j >= 1; j--)
        if(c == t[j - 1]) dp[j] += dp[j - 1];
    }

    return dp[m];
  }
};
```