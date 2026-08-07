# [3348. Smallest Divisible Digit Product II](https://leetcode.com/problems/smallest-divisible-digit-product-ii/)  

<code>Hard</code> level

You are given a string <code>num</code> which represents a **positive** integer, and an integer <code>t</code>.

A number is called **zero-free** if *none* of its digits are 0.

Return a string representing the **smallest zero-free** number greater than or equal to <code>num</code> such that the **product of its digits** is divisible by <code>t</code>. If no such number exists, return <code>"-1"</code>.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> num = "1234", t = 256
<strong>Output:</strong> "1488"
</pre>
**Explanation:**

The smallest zero-free number that is greater than 1234 and has the product of its digits divisible by 256 is 1488, with the product of its digits equal to 256.

**Example 2:**
<pre>
<strong>Input:</strong> num = "12355", t = 50
<strong>Output:</strong> "12355"
</pre>
**Explanation:**

12355 is already zero-free and has the product of its digits divisible by 50, with the product of its digits equal to 150.

**Example 3:**
<pre>
<strong>Input:</strong> num = "11111", t = 26
<strong>Output:</strong> "-1"
</pre>
**Explanation:**

No number greater than 11111 has the product of its digits divisible by 26.

<br />

**Constraints:**

* <code>2 <= num.length <= 2 * 10<sup>5</sup></code>
* <code>num</code> consists only of digits in the range <code>['0', '9']</code>.
* <code>num</code> does not contain leading zeros.
* <code>1 <= t <= 10<sup>14</sup></code>

<br />

***  

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(n)</code>  

**C++**
```C++
class Solution {
  using A = array<int, 4>;

  A factor[10] = 
  {
    {0, 0, 0, 0},
    {0, 0, 0, 0},
    {1, 0, 0, 0},
    {0, 1, 0, 0},
    {2, 0, 0, 0},
    {0, 0, 1, 0},
    {1, 1, 0, 0},
    {0, 0, 0, 1},
    {3, 0, 0, 0},
    {0, 2, 0, 0}
  };

  A missing(const A& need, const A& have) 
  {
    A res;

    for (int i = 0; i < 4; i++) 
    {
      res[i] = max(0, need[i] - have[i]);
    }

    return res;
  }

  string build(A cnt) 
  {
    int c2 = cnt[0];
    int c3 = cnt[1];
    int c5 = cnt[2];
    int c7 = cnt[3];

    int d[10] = {};

    d[8] = c2 / 3;
    c2 %= 3;

    d[9] = c3 / 2;
    c3 %= 2;

    d[4] = c2 / 2;
    c2 %= 2;

    d[2] = c2;
    d[3] = c3;

    if (d[2] && d[3]) 
    {
      d[2]--;
      d[3]--;
      d[6]++;
    }

    if (d[3] && d[4]) 
    {
      d[3]--;
      d[4]--;
      d[2]++;
      d[6]++;
    }

    d[5] = c5;
    d[7] = c7;

    string res;

    for (int digit = 2; digit <= 9; digit++) 
    {
      res += string(d[digit], char('0' + digit));
    }

    return res;
  }

  int requiredDigits(const A& cnt) 
  {
    return build(cnt).size();
  }

public:
  string smallestNumber(string num, long long t) 
  {
    A need = {0, 0, 0, 0};
    int primes[4] = {2, 3, 5, 7};

    for (int i = 0; i < 4; ++i) 
    {
      while (t % primes[i] == 0) 
      {
        need[i]++;
        t /= primes[i];
      }
    }

    if (t != 1) return "-1";

    int n = num.size();
    string minimum = build(need);

    if (minimum.size() > n) return minimum;

    A prefix = {0, 0, 0, 0};
    int firstZero = n;

    for (int i = 0; i < n; ++i) 
    {
      int d = num[i] - '0';

      if (d == 0 && firstZero == n) firstZero = i;

      for (int j = 0; j < 4; ++j) 
      {
        prefix[j] += factor[d][j];
      }
    }

    if (firstZero == n) 
    {
      bool ok = true;

      for (int j = 0; j < 4; ++j) 
      {
        if (prefix[j] < need[j]) ok = false;
      }

      if (ok) return num;
    }

    for (int i = n - 1; i >= 0; --i) 
    {
      int oldDigit = num[i] - '0';

      for (int j = 0; j < 4; ++j) 
      {
          prefix[j] -= factor[oldDigit][j];
      }

      if (i > firstZero) continue;              

      int spaces = n - i - 1;

      for (int d = oldDigit + 1; d <= 9; ++d) 
      {
        A have = prefix;

        for (int j = 0; j < 4; ++j) 
        {
            have[j] += factor[d][j];
        }

        A left = missing(need, have);
        string suffix = build(left);

        if (suffix.size() > spaces) continue;

        int ones = spaces - suffix.size();

        return num.substr(0, i) + char('0' + d) + string(ones, '1') + suffix;
      }
    }

    string suffix = build(need);

    return string(n + 1 - suffix.size(), '1') + suffix;
  }
};
```