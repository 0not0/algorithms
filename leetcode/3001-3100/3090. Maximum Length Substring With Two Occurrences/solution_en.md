# [3090. Maximum Length Substring With Two Occurrences](https://leetcode.com/problems/maximum-length-substring-with-two-occurrences/)

<code>Easy</code> level


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