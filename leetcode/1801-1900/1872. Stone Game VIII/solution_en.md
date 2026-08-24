# [1872. Stone Game VIII](https://leetcode.com/problems/stone-game-viii)  

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    int stoneGameVIII(vector<int>& stones)
    {
      int n = stones.size();
      int best = stones[n - 1];

      for(int i = 1; i < n; i++) stones[i] += stones[i - 1];

      for(int i = n - 2; i >= 1; i--) best = max(best, stones[i] - best);

      return best;
    }
};
```
