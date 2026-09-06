# [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

`Hard` level 

Given two strings s and t, return *the number of distinct **subsequences** of s which equals t*.

The test cases are generated so that the answer fits on a 32-bit signed integer.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "rabbbit", t = "rabbit"
<strong>Output:</strong> 3
</pre>

**Explanation:**  
As shown below, there are 3 ways you can generate "rabbit" from s.    
<code><ins>rabb</ins>b<ins>it</ins></code>  
<code><ins>ra</ins>b<ins>bbit</ins></code>  
<code><ins>rab</ins>b<ins>bit</ins></code>  

**Example 2:**
<pre>
<strong>Input:</strong> s = "babgbag", t = "bag"
<strong>Output:</strong> 5
</pre>

**Explanation:**  
As shown below, there are 5 ways you can generate "bag" from s.  
<code><ins>ba</ins>b**g**bag</code>  
<code><ins>ba</ins>bgba**g**</code>  
<code><ins>b</ins>abgb<ins>a<ins>g</code>  
<code>ba<ins>b</ins>gb<ins>a</ins>**g**</code>  
<code>babg<ins>ba</ins>**g**</code>  

<br />

**Constraints:**

* `1 <= s.length, t.length <= 1000`
* `s` and `t` consist of English letters.

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