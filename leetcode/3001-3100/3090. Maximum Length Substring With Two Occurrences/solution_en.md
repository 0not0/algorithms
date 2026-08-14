# [3090. Maximum Length Substring With Two Occurrences](https://leetcode.com/problems/maximum-length-substring-with-two-occurrences/)

<code>Easy</code> level

Given a string <code>s</code>, return the **maximum** length of a **substring**<sup>1</sup> such that it contains *at most two occurrences* of each character.  

**1.** A **substring** is a contiguous sequence of characters within a string.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "bcbbbcba"
<strong>Output:</strong> 4
</pre>

**Explanation:**

The following substring has a length of 4 and contains at most two occurrences of each character: <code>"bcbbbcba"</code>.

**Example 2:**
<pre>
<strong>Input:</strong> s = "aaaa"
<strong>Output:</strong> 2
</pre>

**Explanation:**

The following substring has a length of 2 and contains at most two occurrences of each character: <code>"aaaa"</code>.

<br />

**Constraints:**

* <code>2 <= s.length <= 100</code>
* <code>s</code> consists only of lowercase English letters.

<br />

***

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**
```C++
class Solution 
{
  public:
    int maximumLengthSubstring(string s)
    {
      int freq[26] = {};
      int left = 0;
      int ans = 0;

      for(int right = 0; right < s.size(); right++)
      {
        freq[s[right] - 'a']++;

        while(freq[s[right] - 'a'] > 2)
        {
            freq[s[left++] - 'a']--;
        }

        ans = max(ans, right - left + 1);
      }

      return ans;
    }
};
```