# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)  

**Medium** level  

Given a string <code>s</code>, find the length of the **longest** **substring**<sup>1</sup> without duplicate characters.  

**1.** A **substring** is a contiguous **non-empty** sequence of characters within a string.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "abcabcbb"
<strong>Output:</strong> 3
</pre>
**Explanation:** The answer is "abc", with the length of 3. Note that <code>"bca"</code> and <code>"cab"</code> are also correct answers.

**Example 2:**
<pre>
<strong>Input:</strong> s = "bbbbb"
<strong>Output:</strong> 1
</pre>
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**
<pre>
<strong>Input:</strong> s = "pwwkew"
<strong>Output:</strong> 3
</pre>
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
</pre>

<br />

**Constraints:**

* <code>0 <= s.length <= 10<sup>5</sup></code>
* <code>s</code> consists of English letters, digits, symbols and spaces.

<br />

***  

**Solution**

**Time complexity:**  <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution 
{
  public:
    int lengthOfLongestSubstring(string s) 
    {
      vector<int> last(256, -1);

      int left = 0;
      int ans = 0;

      for (int right = 0; right < s.size(); right++) 
      {
        unsigned char c = s[right];

        left = max(left, last[c] + 1);

        last[c] = right;

        ans = max(ans, right - left + 1);
      }

      return ans;
    }
};
```