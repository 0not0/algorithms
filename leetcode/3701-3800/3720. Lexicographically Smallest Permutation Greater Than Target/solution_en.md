# [3720. Lexicographically Smallest Permutation Greater Than Target](https://leetcode.com/problems/lexicographically-smallest-permutation-greater-than-target)  

<code>Medium</code> level  



<br />

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(n)</code>  

**C++**
```C++
class Solution
{
  public:
    string lexGreaterPermutation(string s, string target)
    {
      int n = s.size();
      int freq[26] = {};

      for (char c : s) freq[c - 'a']++;

      string res;
      res.reserve(n);

      int i = 0;

      while(i < n && freq[target[i] - 'a'] > 0)
      {
        res.push_back(target[i]);
        freq[target[i] - 'a']--;
        i++;
      }

      for(int pos = i; pos >= 0; pos--)
      {
        if (pos < i)
        {
          freq[target[pos] - 'a']++;
          res.pop_back();
        }

        if(pos == n) continue;

        for(int c = target[pos] - 'a' + 1; c < 26; c++)
        {
          if(freq[c] == 0) continue;

          res.push_back(char('a' + c));
          freq[c]--;

          for(int x = 0; x < 26; x++) res.append(freq[x], char('a' + x));

          return res;
        }
      }

      return "";
    }
};
```