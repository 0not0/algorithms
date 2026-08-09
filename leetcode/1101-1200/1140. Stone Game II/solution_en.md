# [1140. Stone Game II](https://leetcode.com/problems/stone-game-ii/)  

<code>Medium</code> level 

Alice and Bob continue their games with piles of stones. There are a number of piles **arranged in a row**, and each pile has a positive integer number of stones <code>piles[i]</code>. The objective of the game is to end with the most stones.

Alice and Bob take turns, with Alice starting first.

On each player's turn, that player can take **all the stones** in the **first** <code>X</code> remaining piles, where <code>1 <= X <= 2M</code>. Then, we set <code>M = max(M, X)</code>. Initially, M = 1.

The game continues until all the stones have been taken.

Assuming Alice and Bob play optimally, return the maximum number of stones Alice can get.

<br/> 

**Example 1:**
<pre>
<strong>Input:</strong> piles = [2,7,9,4,4]
<strong>Output:</strong> 10
</pre>
**Explanation:**

* If Alice takes one pile at the beginning, Bob takes two piles, then Alice takes 2 piles again. Alice can get <code>2 + 4 + 4 = 10</code> stones in total.
* If Alice takes two piles at the beginning, then Bob can take all three piles left. In this case, Alice get <code>2 + 7 = 9</code> stones in total.  

So we return 10 since it's larger.

**Example 2:**
<pre>
<strong>Input:</strong> piles = [1,2,3,4,5,100]
<strong>Output:</strong> 104
</pre>

<br />

**Constraints:**

* <code>1 <= piles.length <= 100</code>
* <code>1 <= piles[i] <= 10<sup>4</sup></code>

<br />

***

**Solution**  

**Time complexity:** <code>O(n<sup>3</sup>)</code>  
**Space complexity:** <code>O(n<sup>2</sup>)</code>

**C++**  
```C++
class Solution 
{
  public:
    int stoneGameII(vector<int>& piles) 
    {
      int n = piles.size();

      vector<int> suffix(n + 1);
      vector<vector<int>> memo(n, vector<int>(n + 1));

      for(int i = n - 1; i >= 0; i--)
      {
        suffix[i] = suffix[i + 1] + piles[i];
      }

      auto dfs = [&](auto&& dfs, int i, int M) -> int 
      {
        if(i + 2 * M >= n) return suffix[i];
        if(memo[i][M]) return memo[i][M];

        int best = 0;

        for(int x = 1; x <= 2 * M; x++)
        {
          best = max(best, suffix[i] - dfs(dfs, i + x, max(M, x)));
        }

        return memo[i][M] = best;
      };

      return dfs(dfs, 0, 1);
    }
};
```