# [3734. Lexicographically Smallest Palindromic Permutation Greater Than Target](https://leetcode.com/problems/lexicographically-smallest-palindromic-permutation-greater-than-target)

<code>Hard</code> level  

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(n)</code>  

**C++**
```C++
class Solution
{
  public:
    string lexPalindromicPermutation(string s, string target)
    {
      int n = s.size();
      int freq[26] = {};

      for(char c : s) freq[c - 'a']++;

      int oddCount = 0;
      char middle = 0;

      for(int c = 0; c < 26; c++)
      {
        if(freq[c] % 2)
        {
          oddCount++;
          middle = 'a' + c;
        }
      }

      if(oddCount != n % 2) return "";

      int halfFreq[26] = {};

      for(int c = 0; c < 26; c++) halfFreq[c] = freq[c] / 2;

      int halfLen = n / 2;
      string half;
      half.reserve(halfLen);

      int i = 0;

      while(i < halfLen)
      {
        int c = target[i] - 'a';

        if(halfFreq[c] == 0) break;

        half.push_back(target[i]);
        halfFreq[c]--;
        i++;
      }

      auto buildPalindrome = [&](const string& left)
      {
        string res = left;

        if(n % 2) res.push_back(middle);

        for(int j = left.size() - 1; j >= 0; j--) res.push_back(left[j]);

        return res;
      };

      if(i == halfLen)
      {
        string candidate = buildPalindrome(half);

        if(candidate > target) return candidate;
      }

      int pos = min(i, halfLen - 1);

      for(; pos >= 0; pos--)
      {
        if(pos < i)
        {
          halfFreq[half.back() - 'a']++;
          half.pop_back();
        }

        int current = target[pos] - 'a';

        for(int c = current + 1; c < 26; c++)
        {
          if(halfFreq[c] == 0) continue;

          string left = half;
          left.push_back('a' + c);
          halfFreq[c]--;

          for(int x = 0; x < 26; x++) left.append(halfFreq[x], 'a' + x);

          return buildPalindrome(left);
        }
      }

      return "";
    }
};
```