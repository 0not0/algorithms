# [2029. Stone Game IX](https://leetcode.com/problems/stone-game-ix/)


<br />

***

**Solution**  

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>

**C++**  
```C++
class Solution 
{
  public:
    bool stoneGameIX(vector<int>& stones) 
    {
      int cnt[3] = {};

      for(int i : stones) cnt[i % 3]++;

      return cnt[0] % 2 == 0
        ? cnt[1] > 0 && cnt[2] > 0
        : abs(cnt[1] - cnt[2]) > 2;
    }
};
```