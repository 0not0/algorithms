# [1510. Stone Game IV](https://leetcode.com/problems/stone-game-iv/)

<code>Hard</code> level  

Alice and Bob take turns playing a game, with Alice starting first.

Initially, there are <code>n</code> stones in a pile. On each player's turn, that player makes a *move* consisting of removing **any** non-zero **square number** of stones in the pile.

Also, if a player cannot make a move, he/she loses the game.

Given a positive integer <code>n</code>, return <code>true</code> if and only if Alice wins the game otherwise return <code>false</code>, assuming both players play optimally.  

<br />

**Example 1:**
<pre>
Input: n = 1
Output: true
Explanation: Alice can remove 1 stone winning the game because Bob doesn't have any moves.
</pre>

**Example 2:**
<pre>
Input: n = 2
Output: false
Explanation: Alice can only remove 1 stone, after that Bob removes the last one winning the game (2 -> 1 -> 0).
</pre>

**Example 3:**
<pre>
Input: n = 4
Output: true
Explanation: n is already a perfect square, Alice can win with one move, removing 4 stones (4 -> 0).
</pre>

<br />

**Constraints:**

* <code>1 <= n <= 10<sup>5</sup></code>  

<br />

***

### Solution  

**Time complexity:**  <code>O(n * sqrt(n))</code>  
**Space complexity:**  <code>O(n)</code>   

**C++**  
```C++
class Solution 
{
  public:
    bool winnerSquareGame(int n) 
    {
      vector<int> squares;
      vector<bool> dp(n + 1, false);

      for(int x = 1; x * x <= n; x++) 
      {
        squares.push_back(x * x);
      }

      for(int i = 1; i <= n; i++)
      {
        for(int sq : squares)
        {
          if(sq > i) break;

          if(!dp[i - sq]) 
          {
            dp[i] = true;
            break;
          }
        }
      }

      return dp[n];
    }
};
```