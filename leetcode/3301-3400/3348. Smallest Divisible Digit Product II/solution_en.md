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