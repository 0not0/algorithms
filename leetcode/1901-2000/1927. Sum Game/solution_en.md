# [1927. Sum Game](https://leetcode.com/problems/sum-game)

<code>Medium</code> level  

Alice and Bob take turns playing a game, with **Alice starting first**.

You are given a string <code>num</code> of even length consisting of digits and <code>'?'</code> characters. On each turn, a player will do the following if there is still at least one <code>'?'</code> in <code>num</code>:

1. Choose an index <code>i</code> where <code>num[i] == '?'</code>.
2. Replace <code>num[i]</code> with any digit between <code>'0'</code> and <code>'9'</code>.  

The game ends when there are no more <code>'?'</code> characters in <code>num</code>.

For Bob to win, the sum of the digits in the first half of <code>num</code> must be **equal** to the sum of the digits in the second half. For Alice to win, the sums must **not be equal**.

* For example, if the game ended with <code>num = "243801"</code>, then Bob wins because <code>2+4+3 = 8+0+1</code>. If the game ended with <code>num = "243803"</code>, then Alice wins because <code>2+4+3 != 8+0+3</code>.  
  
Assuming Alice and Bob play **optimally**, return <code>true</code> *if Alice will win and* <code>false</code> *if Bob will win*.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> num = "5023"
<strong>Output:</strong> false
<strong>Explanation:</strong> There are no moves to be made.
The sum of the first half is equal to the sum of the second half: 5 + 0 = 2 + 3.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> num = "25??"
<strong>Output:</strong> true
<strong>Explanation:</strong> Alice can replace one of the '?'s with '9' and it will be impossible for Bob to make the sums equal.  
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> num = "?3295???"
<strong>Output:</strong> false
<strong>Explanation:</strong> It can be proven that Bob will always win. One possible outcome is:
- Alice replaces the first '?' with '9'. num = "93295???".
- Bob replaces one of the '?' in the right half with '9'. num = "932959??".
- Alice replaces one of the '?' in the right half with '2'. num = "9329592?".
- Bob replaces the last '?' in the right half with '7'. num = "93295927".
Bob wins because 9 + 3 + 2 + 9 = 5 + 9 + 2 + 7.
</pre>

<br />

**Constraints:**

* <code>2 <= num.length <= 10<sup>5</sup></code>
* <code>num.length</code> is **even**.
* <code>num</code> consists of only digits and <code>'?'</code>.  

<br />

***  

### Solution

**Time complexity:** <code>O(log n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    bool sumGame(string num)
    {
      int n = num.size();

      int diff = 0;
      int qDiff = 0;
      int total = 0;

      for(int i = 0; i < n; i++)
      {
        int sign = i < n / 2 ? 1 : -1;

        if(num[i] == '?')
        {
          qDiff += sign;
          total++;
        } else
        {
          diff += sign * (num[i] - '0');
        }
      }

      if(total % 2) return true;

      return 2 * diff != -9 * qDiff;
    }
};
```