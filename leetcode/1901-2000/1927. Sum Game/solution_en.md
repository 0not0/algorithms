# [1927. Sum Game](https://leetcode.com/problems/sum-game)


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