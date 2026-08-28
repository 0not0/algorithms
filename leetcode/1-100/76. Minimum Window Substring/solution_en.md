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

### Solution

**Time complexity:**  <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution 
{
  public:
    string minWindow(string s, string t) {
      int need[128] = {};

      for(char c : t) need[c]++;
      
      int left = 0;
      int required = t.size();

      int minStart = 0;
      int minLength = INT_MAX;

        for (int right = 0; right < s.size(); right++)
        {
          char c = s[right];

          if (need[c] > 0) required--;

          need[c]--;

          while(required == 0)
          {
            int length = right - left + 1;

            if(length < minLength)
            {
              minLength = length;
              minStart = left;
            }

            char leftChar = s[left];
            need[leftChar]++;

            if(need[leftChar] > 0) required++;

            left++;
          }
        }

      return minLength == INT_MAX ? "" : s.substr(minStart, minLength);
    }
};
```

**JavaScript**
```JS
var minWindow = function(s, t) {
  const need = new Array(128).fill(0);

  for(const c of t) need[c.charCodeAt(0)]++;

  let left = 0;
  let required = t.length;

  let minStart = 0;
  let minLength = Infinity;

  for(let right = 0; right < s.length; right++) {
    const code = s.charCodeAt(right);

    if(need[code] > 0) required--;

    need[code]--;

    while(required === 0) {
      const length = right - left + 1;

      if(length < minLength) {
        minLength = length;
        minStart = left;
      }

      const leftCode = s.charCodeAt(left);

      need[leftCode]++;

      if(need[leftCode] > 0) required++;

      left++;
    }
  }

  return minLength === Infinity ? "" : s.slice(minStart, minStart + minLength);
};
```