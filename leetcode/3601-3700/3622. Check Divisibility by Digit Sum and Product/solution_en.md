# [3622. Check Divisibility by Digit Sum and Product](https://leetcode.com/problems/check-divisibility-by-digit-sum-and-product) 

***  

### Solution

**Time complexity:** <code>O(logn)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    bool checkDivisibility(int n)
    {
      int x = n;
      int sum = 0;
      int product = 1;

      while(x)
      {
        int d = x % 10;
        sum += d;
        product *= d;
        x /= 10;
      }

      return n % (sum + product) == 0;
    }
};
```