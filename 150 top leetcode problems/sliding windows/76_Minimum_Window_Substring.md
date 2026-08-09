# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

**Hard** level 

Given two strings <code>s</code> and <code>t</code> of lengths <code>m</code> and <code>n</code> respectively, return *the **minimum window** **substring***<sup>1</sup> *of* <code>s</code> *such that every character in* <code>t</code> *(**including duplicates**) is included in the window*. If there is no such substring, return the empty string <code>""</code>.

The testcases will be generated such that the answer is **unique**.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "ADOBECODEBANC", t = "ABC"
<strong>Output:</strong> "BANC"
<strong>Explanation:</strong> The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> s = "a", t = "a"
<strong>Output:</strong> "a"
<strong>Explanation:</strong> The entire string s is the minimum window.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> s = "a", t = "aa"
<strong>Output:</strong> ""
<strong>Explanation:</strong> Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
</pre>

<br />

**Constraints:**

* <code>m == s.length</code>
* <code>n == t.length</code>
* <code>1 <= m, n <= 10<sup>5</sup></code>
* <code>s</code> and <code>t</code> consist of uppercase and lowercase English letters.  

<br />

**Follow up:** Could you find an algorithm that runs in <code>O(m + n)</code> time?  

<br />

***  

**Solution**

**Time complexity:**  
**Space complexity:** 

**C++**
```C++

```