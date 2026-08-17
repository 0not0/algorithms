# [1563. Stone Game V](https://leetcode.com/problems/stone-game-v/)


***  

### Solution

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