# [2029. Stone Game IX](https://leetcode.com/problems/stone-game-ix/)

Alice and Bob continue their games with stones. There is a row of n stones, and each stone has an associated value. You are given an integer array <code>stones</code>, where <code>stones[i]</code> is the **value** of the <code>i<sup>th</sup></code> stone.

Alice and Bob take turns, with **Alice** starting first. On each turn, the player may remove any stone from <code>stones</code>. The player who removes a stone **loses** if the **sum** of the values of **all removed stones** is divisible by <code>3</code>. Bob will win automatically if there are no remaining stones (even if it is Alice's turn).

Assuming both players play **optimally**, return <code>true</code> *if Alice wins and* <code>false</code> *if Bob wins*.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> stones = [2,1]
<strong>Output:</strong> true
<strong>Explanation:</strong> The game will be played as follows:
- Turn 1: Alice can remove either stone.
- Turn 2: Bob removes the remaining stone. 
The sum of the removed stones is 1 + 2 = 3 and is divisible by 3. Therefore, Bob loses and Alice wins the game.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> stones = [2]
<strong>Output:</strong> false
<strong>Explanation:</strong> Alice will remove the only stone, and the sum of the values on the removed stones is 2. 
Since all the stones are removed and the sum of values is not divisible by 3, Bob wins the game.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> stones = [5,1,2,4,3]
<strong>Output:</strong> false
<strong>Explanation:</strong> Bob will always win. One possible way for Bob to win is shown below:
- Turn 1: Alice can remove the second stone with value 1. Sum of removed stones = 1.
- Turn 2: Bob removes the fifth stone with value 3. Sum of removed stones = 1 + 3 = 4.
- Turn 3: Alices removes the fourth stone with value 4. Sum of removed stones = 1 + 3 + 4 = 8.
- Turn 4: Bob removes the third stone with value 2. Sum of removed stones = 1 + 3 + 4 + 2 = 10.
- Turn 5: Alice removes the first stone with value 5. Sum of removed stones = 1 + 3 + 4 + 2 + 5 = 15.
Alice loses the game because the sum of the removed stones (15) is divisible by 3. Bob wins the game.
</pre>

<br />

**Constraints:**

* <code>1 <= stones.length <= 10<sup>5</sup></code>
* <code>1 <= stones[i] <= 10<sup>4</sup></code>

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