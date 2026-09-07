# [940. Distinct Subsequences II](https://leetcode.com/problems/distinct-subsequences-ii/)  

`Hard` level  

Given a string s, return *the number of **distinct non-empty subsequences** of* `s`. Since the answer may be very large, return it **modulo** <code>10<sup>9</sup> + 7</code>.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "abc"
<strong>Output:</strong> 7
<strong>Explanation:</strong> The 7 distinct subsequences are "a", "b", "c", "ab", "ac", "bc", and "abc".
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> s = "aba"
<strong>Output:</strong> 6
<strong>Explanation:</strong> The 6 distinct subsequences are "a", "b", "ab", "aa", "ba", and "aba".
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> s = "aaa"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The 3 distinct subsequences are "a", "aa" and "aaa".
</pre>

<br />

**Constraints:**

* `1 <= s.length <= 2000`
* `s` consists of lowercase English letters.

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