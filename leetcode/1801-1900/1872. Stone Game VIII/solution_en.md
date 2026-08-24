# [1872. Stone Game VIII](https://leetcode.com/problems/stone-game-viii)  

<code>Hard</code> level

Alice and Bob take turns playing a game, with **Alice starting first**.

There are <code>n</code> stones arranged in a row. On each player's turn, while the number of stones is **more than one**, they will do the following:

1. Choose an integer <code>x > 1</code>, and **remove** the leftmost <code>x</code> stones from the row.
2. Add the **sum** of the **removed** stones' values to the player's score.
3. Place a **new stone**, whose value is equal to that sum, on the left side of the row. 

The game stops when **only one** stone is left in the row.

The **score difference** between Alice and Bob is <code>(Alice's score - Bob's score)</code>. Alice's goal is to **maximize** the score difference, and Bob's goal is the **minimize** the score difference.

Given an integer array <code>stones</code> of length <code>n</code> where <code>stones[i]</code> represents the value of the <code>i<sup>th</sup></code> stone **from the left**, return *the **score difference** between Alice and Bob if they both play **optimally***.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> stones = [-1,2,-3,4,-5]
<strong>Output:</strong> 5
<strong>Explanation:</strong>
- Alice removes the first 4 stones, adds (-1) + 2 + (-3) + 4 = 2 to her score, and places a stone of
  value 2 on the left. stones = [2,-5].
- Bob removes the first 2 stones, adds 2 + (-5) = -3 to his score, and places a stone of value -3 on
  the left. stones = [-3].
The difference between their scores is 2 - (-3) = 5.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> stones = [7,-6,5,10,5,-2,-6]
<strong>Output:</strong> 13
<strong>Explanation:</strong>
- Alice removes all stones, adds 7 + (-6) + 5 + 10 + 5 + (-2) + (-6) = 13 to her score, and places a stone of value 13 on the left. stones = [13].
The difference between their scores is 13 - 0 = 13.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> stones = [-10,-12]
<strong>Output:</strong> -22
<strong>Explanation:</strong>
- Alice can only make one move, which is to remove both stones. She adds (-10) + (-12) = -22 to her score and places a stone of value -22 on the left. stones = [-22].
The difference between their scores is (-22) - 0 = -22.
</pre>

<br />

**Constraints:**

* <code>n == stones.length</code>
* <code>2 <= n <= 10<sup>5</sup></code>
* <code>-10<sup>4</sup> <= stones[i] <= 10<sup>4</sup></code>

<br />

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
