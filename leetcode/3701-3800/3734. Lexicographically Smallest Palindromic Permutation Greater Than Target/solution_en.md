# [3734. Lexicographically Smallest Palindromic Permutation Greater Than Target](https://leetcode.com/problems/lexicographically-smallest-palindromic-permutation-greater-than-target)

<code>Hard</code> level  

You are given two strings <code>s</code> and <code>target</code>, each of length <code>n</code>, consisting of lowercase English letters.

Return the **lexicographically smallest**<sup>1</sup> **string** that is **both** a **palindromic permutation**<sup>2</sup> of <code>s</code> and **strictly** greater than <code>target</code>. If no such permutation exists, return an empty string.  

**1.** - A string <code>a</code> is **lexicographically smaller** than a string <code>b</code> if in the first position where <code>a</code> and <code>b</code> differ, string <code>a</code> has a letter that appears earlier in the alphabet than the corresponding letter in <code>b</code>.  
If the first <code>min(a.length, b.length)</code> characters do not differ, then the shorter string is the lexicographically smaller one.   

**2.** - A **palindrome** is a string that reads the same forward and backward.  

<br />

**Example 1:**
<pre>
Input: s = "baba", target = "abba"
Output: "baab"
</pre>
**Explanation:**

* The palindromic permutations of <code>s</code> (in lexicographical order) are <code>"abba"</code> and <code>"baab"</code>.
* The lexicographically smallest permutation that is strictly greater than <code>target</code> is <code>"baab"</code>.

**Example 2:**
<pre>
Input: s = "baba", target = "bbaa"
Output: ""
</pre>
**Explanation:**

* The palindromic permutations of <code>s</code> (in lexicographical order) are <code>"abba"</code> and <code>"baab"</code>.
* None of them is lexicographically strictly greater than <code>target</code>. Therefore, the answer is <code>""</code>.

**Example 3:**
<pre>
Input: s = "abc", target = "abb"
Output: ""
</pre>
**Explanation:**

<code>s</code> has no palindromic permutations. Therefore, the answer is <code>""</code>.

**Example 4:**
<pre>
Input: s = "aac", target = "abb"
Output: "aca"
</pre>
**Explanation:**

* The only palindromic permutation of <code>s</code> is <code>"aca"</code>.
* <code>"aca"</code> is strictly greater than target. Therefore, the answer is <code>"aca"</code>.

<br />

**Constraints:**

* <code>1 <= n == s.length == target.length <= 300</code>
* <code>s</code> and <code>target</code> consist of only lowercase English letters.

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