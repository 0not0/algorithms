# [3116. Kth Smallest Amount With Single Denomination Combination](https://leetcode.com/problems/kth-smallest-amount-with-single-denomination-combination/)

<code>Hard</code> level

You are given an integer array <code>coins</code> representing coins of different denominations and an integer <code>k</code>.

You have an infinite number of coins of each denomination. However, you are **not allowed** to combine coins of different denominations.

Return the <code>k<sup>th</sup></code> **smallest** amount that can be made using these coins.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> coins = [3,6,9], k = 3
<strong>Output:</strong> 9
</pre>
**Explanation:** The given coins can make the following amounts:  
Coin 3 produces multiples of 3: 3, 6, 9, 12, 15, etc.  
Coin 6 produces multiples of 6: 6, 12, 18, 24, etc.   
Coin 9 produces multiples of 9: 9, 18, 27, 36, etc.  
All of the coins combined produce: 3, 6, **9**, 12, 15, etc.  

**Example 2:**
<pre>
<strong>Input:</strong> coins = [5,2], k = 7
<strong>Output:</strong> 12
</pre>
**Explanation:** The given coins can make the following amounts:  
Coin 5 produces multiples of 5: 5, 10, 15, 20, etc.  
Coin 2 produces multiples of 2: 2, 4, 6, 8, 10, 12, etc.  
All of the coins combined produce: 2, 4, 5, 6, 8, 10, **12**, 14, 15, etc.  

<br />

**Constraints:**

* <code>1 <= coins.length <= 15</code>
* <code>1 <= coins[i] <= 25</code>
* <code>1 <= k <= 2 * 10<sup>9</sup></code>
* <code>coins</code> contains pairwise distinct integers.

<br />

***  

### Solution

**Time complexity:** <code>O(2<sup>n</sup>(n + log(k · minCoin)))</code>  
**Space complexity:** <code>O(2<sup>n</sup>)</code>  
*where:*  
**n** - starting number of coins  
**minCoin** - the smallest denomination in the array

**C++**
```C++
class Solution
{
  public:
    long long findKthSmallest(vector<int>& coins, int k)
    {
      sort(coins.begin(), coins.end());
      vector<int> filtered;

      for(int c : coins)
      {
        bool redundant = false;

        for(int x : filtered)
        {
          if(c % x == 0)
          {
            redundant = true;
            break;
          }
        }

        if(!redundant) filtered.push_back(c);
      }

      int n = filtered.size();
      long long right = 1LL * filtered[0] * k;
      vector<pair<long long, int>> terms;

      for(int mask = 1; mask < (1 << n); mask++)
      {
        long long lcm = 1;
        int bits = 0;
        bool valid = true;

        for(int i = 0; i < n; i++)
        {
          if(!(mask & (1 << i))) continue;

          bits++;

          long long g = gcd(lcm, (long long)filtered[i]);

          if(lcm / g > right / filtered[i])
          {
            valid = false;
            break;
          }

          lcm = lcm / g * filtered[i];

          if(lcm > right)
          {
            valid = false;
            break;
          }
        }

        if(valid) terms.push_back({lcm, (bits % 2 == 1) ? 1 : -1});   
      }

      auto count = [&](long long x)
      {
        long long total = 0;

        for(auto [lcm, sign] : terms)
        {
          total += sign * (x / lcm);
        }

        return total;
      };

      long long left = 1;

      while(left < right)
      {
        long long mid = left + (right - left) / 2;

        if(count(mid) >= k) right = mid;
        else left = mid + 1;
      }

      return left;
    }
};
```