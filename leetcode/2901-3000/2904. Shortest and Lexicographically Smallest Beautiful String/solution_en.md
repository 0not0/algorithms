# [2904. Shortest and Lexicographically Smallest Beautiful String](https://leetcode.com/problems/shortest-and-lexicographically-smallest-beautiful-string)  

<code>Medium</code> level  
***  

### Solution

**Time complexity:** <code>O(n<sup>2</sup>)</code>  
**Space complexity:** <code>O(1)</code>  
**<sup>*</sup>** but with output string **Space complexity:** is <code>O(n)</code>

**C++**
```C++
class Solution
{
  public:
    string shortestBeautifulSubstring(string s, int k)
    {
      int n = s.size();
      int left = 0;
      int ones = 0;

      int bLeft = -1;
      int bLen = INT_MAX;

      for(int right = 0; right < n; right++)
      {
        ones += s[right] == '1';

        while(ones > k)
        {
            ones -= s[left] == '1';
            left++;
        }

        while(ones == k && s[left] == '0') left++;

        if(ones != k) continue;

        int len = right - left + 1;

        if(
          len < bLen || 
          (len == bLen &&
          lexicographical_compare(s.begin() + left, s.begin() + right + 1, s.begin() + bLeft, s.begin() + bLeft + bLen))
        )
        {
          bLen = len;
          bLeft = left;
        }
      }

    return bLeft == -1 ? "" : s.substr(bLeft, bLen);
  }
};
```