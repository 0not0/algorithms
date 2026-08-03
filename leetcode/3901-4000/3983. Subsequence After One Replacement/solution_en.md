# [3983. Subsequence After One Replacement](https://leetcode.com/problems/subsequence-after-one-replacement/)  

<code>Medium</code> level 

You are given two strings <code>s</code> and <code>t</code> consisting of lowercase English letters.

You may choose **at most** one index in <code>s</code> and replace the character at that index with any lowercase English letter.

Return <code>true</code> if it is possible to make <code>s</code> a <strong>subsequence</strong> of <code>t</code>; otherwise, return <code>false</code>.

**Example 1:**
<pre>
<strong>Input:</strong> s = "cat", t = "chat"
<strong>Output:</strong> true
</pre>
**Explanation:**

* Replace <code>s[1]</code> from <code>'a'</code> to <code>'h'</code>. The resulting string is <code>"cht"</code>.
* <code>"cht"</code> is a subsequence of <code>"chat"</code> because we can match <code>'c'</code>, <code>'h'</code>, and <code>'t'</code> in order.  
<br />

**Example 2:**
<pre>
<strong>Input:</strong> s = "plane", t = "apple"
<strong>Output:</strong> false
</pre>
**Explanation:**

* The characters <code>'p'</code>, <code>'l'</code>, and <code>'e'</code> can be matched in <code>t</code>, but the remaining characters cannot be matched while preserving the required order.
* Even after replacing any one character in <code>s</code>, it is impossible to make <code>s</code> a subsequence of <code>t</code>.  
<br />

**Constraints:**

* <code>1 <= s.length, t.length <= 10<sup>5</sup></code>
* <code>s</code> and <code>t</code> consist only of lowercase English letters.

<br />

***  

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**
```C++
class Solution {
public:
  bool canMakeSubsequence(string s, string t) {
    int without = 0;
    int with = 0;

    for (char c : t) {
      if (with < s.size() && s[with] == c) with++;

      if (without < s.size()) {
        with = max(with, without + 1);

        if (s[without] == c) {
          without++;
        }
      }
    }

    return max(without, with) == s.size();
  }
};
```