# [3302. Find the Lexicographically Smallest Valid Sequence](https://leetcode.com/problems/find-the-lexicographically-smallest-valid-sequence/)  

<code>Medium</code> level  

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

      for (int i = n - 1; i >= 0 && j >= 0; i--) 
      {
        if (word1[i] == word2[j]) 
        {
          suf[j] = i;
          j--;
        }
      }

      int i = 0;
      j = 0;
      bool used = false;

      while (i < n && j < m) 
      {
        if (word1[i] == word2[j]) 
        {
          ans.push_back(i);
          i++;
          j++;
        } 
        else if (!used && (j == m - 1 || suf[j + 1] > i)) 
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