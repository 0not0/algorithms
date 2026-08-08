# [3302. Find the Lexicographically Smallest Valid Sequence](https://leetcode.com/problems/find-the-lexicographically-smallest-valid-sequence/)  

<code>Medium</code> level  

You are given two strings <code>word1</code> and <code>word2</code>.

A string <code>x</code> is called **almost equal** to <code>y</code> if you can change **at most** one character in <code>x</code> to make it *identical* to <code>y</code>.

A sequence of indices <code>seq</code> is called **valid** if:

* The indices are sorted in **ascending** order.
* *Concatenating* the characters at these indices in <code>word1</code> in the **same order** results in a string that is **almost equal** to <code>word2</code>.  

Return an array of size <code>word2.length</code> representing the **lexicographicallyx smallest**<sup>1</sup> **valid** sequence of indices. If no such sequence of indices exists, return an **empty** array.

**Note** that the answer must represent the *lexicographically smallest array*, **not** the corresponding string formed by those indices.

**1.** An array <code>a</code> is **lexicographically smaller** than an array <code>b</code> if in the first position where <code>a</code> and <code>b</code> differ, array <code>a</code> has an element that is less than the corresponding element in <code>b</code>.
If the first <code>min(a.length, b.length)</code> elements do not differ, then the shorter array is the lexicographically smaller one.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> word1 = "vbcca", word2 = "abc"
<strong>Output:</strong> [0,1,2]
</pre>
**Explanation:**

The lexicographically smallest valid sequence of indices is <code>[0, 1, 2]</code>:

* Change <code>word1[0]</code> to <code>'a'</code>.
* <code>word1[1]</code> is already <code>'b'</code>.
* <code>word1[2]</code> is already <code>'c'</code>.  

**Example 2:**
<pre>
<strong>Input:</strong> word1 = "bacdc", word2 = "abc"
<strong>Output:</strong> [1,2,4]
</pre>
**Explanation:**

The lexicographically smallest valid sequence of indices is <code>[1, 2, 4]</code>:

* <code>word1[1]</code> is already <code>'a'</code>.
* Change <code>word1[2]</code> to <code>'b'</code>.
* <code>word1[4]</code> is already <code>'c'</code>.  

**Example 3:**
<pre>
<strong>Input:</strong> word1 = "aaaaaa", word2 = "aaabc"
<strong>Output:</strong> []
</pre>
**Explanation:**

There is no valid sequence of indices.

**Example 4:**
<pre>
<strong>Input:</strong> word1 = "abc", word2 = "ab"
<strong>Output:</strong> [0,1]
</pre>  

<br />

**Constraints:**

* <code>1 <= word2.length < word1.length <= 3 * 10<sup>5</sup></code>
* <code>word1</code> and <code>word2</code> consist only of lowercase English letters.  

<br />

***  

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(m)</code>   

**C++**  
```C++
class Solution 
{
  public:
    vector<int> validSequence(string word1, string word2) 
    {
      int n = word1.size();
      int m = word2.size();

      vector<int> suf(m, -1);
      vector<int> ans;

      int j = m - 1;

      for(int i = n - 1; i >= 0 && j >= 0; i--) 
      {
        if(word1[i] == word2[j]) 
        {
          suf[j] = i;
          j--;
        }
      }

      int i = 0;
      j = 0;
      bool used = false;

      while(i < n && j < m) 
      {
        if(word1[i] == word2[j]) 
        {
          ans.push_back(i);
          i++;
          j++;
        } 
        else if(!used && (j == m - 1 || suf[j + 1] > i)) 
        {
          ans.push_back(i);
          used = true;
          i++;
          j++;
        }
        else
        {
          i++;
        }
      }

      return j == m ? ans : vector<int>{};
    }
};
```
