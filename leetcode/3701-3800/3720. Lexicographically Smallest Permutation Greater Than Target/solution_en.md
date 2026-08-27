# [3720. Lexicographically Smallest Permutation Greater Than Target](https://leetcode.com/problems/lexicographically-smallest-permutation-greater-than-target)  

<code>Medium</code> level  

You are given two strings <code>s</code> and <code>target</code>, both having length <code>n</code>, consisting of lowercase English letters.

Return the **lexicographically smallest** **permutation**<sup>1</sup> of <code>s</code> that is **strictly** greater than <code>target</code>. If no permutation of <code>s</code> is lexicographically strictly greater than <code>target</code>, return an empty string.

A string <code>a</code> is **lexicographically strictly greater** than a string <code>b</code> (of the same length) if in the first position where <code>a</code> and <code>b</code> differ, string <code>a</code> has a letter that appears later in the alphabet than the corresponding letter in <code>b</code>.  

**1.** A permutation is a rearrangement of all the characters of a string.  

<br />

**Example 1:**
<pre>
Input: s = "abc", target = "bba"
Output: "bca"
</pre>

**Explanation:**

* The permutations of <code>s</code> (in lexicographical order) are <code>"abc"</code>, <code>"acb"</code>, <code>"bac"</code>, <code>"bca"</code>, <code>"cab"</code>, and <code>"cba"</code>.
* The lexicographically smallest permutation that is strictly greater than <code>target</code> is <code>"bca"</code>.

**Example 2:**
<pre>
Input: s = "leet", target = "code"
Output: "eelt"
</pre>

**Explanation:**

* The permutations of <code>s</code> (in lexicographical order) are <code>"eelt"</code>, <code>"eetl"</code>, <code>"elet"</code>, <code>"elte"</code>, <code>"etel"</code>, <code>"etle"</code>, <code>"leet"</code>, <code>"lete"</code>, <code>"ltee"</code>, <code>"teel"</code>, <code>"tele"</code>, and <code>"tlee"</code>.
* The lexicographically smallest permutation that is strictly greater than <code>target</code> is <code>"eelt"</code>.

**Example 3:**
<pre>
Input: s = "baba", target = "bbaa"
Output: ""
</pre>

**Explanation:**

* The permutations of <code>s</code> (in lexicographical order) are <code>"aabb"</code>, <code>"abab"</code>, <code>"abba"</code>, <code>"baab"</code>, <code>"baba"</code>, and <code>"bbaa"</code>.
* None of them is lexicographically strictly greater than <code>target</code>. Therefore, the answer is <code>""</code>.

<br />

**Constraints:** 

* <code>1 <= s.length == target.length <= 300</code>
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