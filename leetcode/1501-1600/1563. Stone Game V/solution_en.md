# [1563. Stone Game V](https://leetcode.com/problems/stone-game-v/)

<code>Hard</code> level  

There are several stones **arranged in a row**, and each stone has an associated value which is an integer given in the array <code>stoneValue</code>.

In each round of the game, Alice divides the row into **two non-empty rows** (i.e. left row and right row), then Bob calculates the value of each row which is the sum of the values of all the stones in this row. Bob throws away the row which has the maximum value, and Alice's score increases by the value of the remaining row. If the value of the two rows are equal, Bob lets Alice decide which row will be thrown away. The next round starts with the remaining row.

The game ends when there is only **one stone remaining**. Alice's score is initially **zero**.

Return *the maximum score that Alice can obtain*.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> stoneValue = [6,2,3,4,5,5]
<strong>Output:</strong> 18
<strong>Explanation:</strong> In the first round, Alice divides the row to [6,2,3], [4,5,5]. The left row has the value 11 and the right row has value 14. Bob throws away the right row and Alice's score is now 11.
In the second round Alice divides the row to [6], [2,3]. This time Bob throws away the left row and Alice's score becomes 16 (11 + 5).
The last round Alice has only one choice to divide the row which is [2], [3]. Bob throws away the right row and Alice's score is now 18 (16 + 2). The game ends because only one stone is remaining in the row.  
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> stoneValue = [7,7,7,7,7,7,7]
<strong>Output:</strong> 28
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> stoneValue = [4]
<strong>Output:</strong> 0
</pre>

<br />

**Constraints:**

* <code>1 <= stoneValue.length <= 500</code>
* <code>1 <= stoneValue[i] <= 10<sup>6</sup></code>

<br />

***  

### Solution

There are two solutions depending on **Time complexity**: <code>O(n<sup>3</sup>)</code> or <code>O(n<sup>2</sup>)</code>. First one (<code>O(n<sup>3</sup>)</code>) is more readable.  

**Time complexity:** <code>O(n<sup>3</sup>)</code>  
**Space complexity:** <code>O(n<sup>2</sup>)</code>  

**C++**
```C++
class Solution 
{
  public:
    int stoneGameV(vector<int>& stoneValue) 
    {
      int n = stoneValue.size();
      vector<int> prefix(n + 1);

      for (int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + stoneValue[i];

      vector<vector<int>> dp(n, vector<int>(n, 0));

      auto sum = [&](int l, int r) { return prefix[r + 1] - prefix[l]; };

      for(int len = 2; len <= n; len++) 
      {
        for(int l = 0; l + len <= n; l++) 
        {
          int r = l + len - 1;

          for(int m = l; m < r; m++) 
          {
            int leftSum = sum(l, m);
            int rightSum = sum(m + 1, r);

            if(leftSum < rightSum) dp[l][r] = max(dp[l][r], leftSum + dp[l][m]);
            else if(leftSum > rightSum) dp[l][r] = max(dp[l][r], rightSum + dp[m + 1][r]);
            else dp[l][r] = max(dp[l][r], leftSum + max(dp[l][m], dp[m + 1][r]));
          }
        }
      }

      return dp[0][n - 1];
    }
};
```
**Time complexity:** <code>O(n<sup>2</sup>)</code>    
**Space complexity:** <code>O(n<sup>2</sup>)</code>  

**C++**
```C++
class Solution 
{
  public:
    int stoneGameV(vector<int>& stoneValue) 
    {
      int n = stoneValue.size();
      vector<int> prefix(n + 1);

      for(int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + stoneValue[i];

      vector<vector<int>> dp(n, vector<int>(n));
      vector<int> mid(n);

      for(int i = 0; i < n; i++) 
      {
        mid[i] = i;
        dp[i][i] = stoneValue[i];
      }

      int answer = 0;

      for(int len = 2; len <= n; len++) 
      {
          for(int i = 0; i + len <= n; i++) 
          {
            int j = i + len - 1;

            while(mid[i] <= j && prefix[mid[i]] - prefix[i] < prefix[j + 1] - prefix[mid[i]]) 
              mid[i]++;

            int p = mid[i];
            int best = 0;

            int leftSum = prefix[p] - prefix[i];
            int rightSum = prefix[j + 1] - prefix[p];

            if(leftSum == rightSum) best = max(dp[i][p - 1], dp[j][p]);
            else if(i <= p - 2) best = max(best,dp[i][p - 2]);
            
            if(p <= j) best = max(best, dp[j][p]);

            int total = prefix[j + 1] - prefix[i];

            dp[i][j] = max(dp[i][j - 1], total + best);
            dp[j][i] = max(dp[j][i + 1], total + best);

            answer = best;
          }
      }

      return answer;
    }
};
```