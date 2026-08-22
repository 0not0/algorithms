# [3622. Check Divisibility by Digit Sum and Product](https://leetcode.com/problems/check-divisibility-by-digit-sum-and-product) 

<code>Easy</code> level

You are given a positive integer <code>n</code>. Determine whether n is divisible by the **sum** of the following two values:

* The **digit sum** of <code>n</code> (the sum of its digits).

* The **digit product** of <code>n</code> (the product of its digits).

Return <code>true</code> if <code>n</code> is divisible by this sum; otherwise, return <code>false</code>.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> n = 99
<strong>Output:</strong> true
<strong>Explanation:</strong>

Since 99 is divisible by the sum (9 + 9 = 18) plus product (9 * 9 = 81) of its digits (total 99), the output is true.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> n = 23
<strong>Output:</strong> false
<strong>Explanation:</strong>

Since 23 is not divisible by the sum (2 + 3 = 5) plus product (2 * 3 = 6) of its digits (total 11), the output is false.
</pre>

<br />

**Constraints:**

* <code>1 <= n <= 10<sup>6</sup></code>

<br />

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