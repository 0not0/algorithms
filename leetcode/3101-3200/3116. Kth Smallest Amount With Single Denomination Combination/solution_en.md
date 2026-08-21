# [3116. Kth Smallest Amount With Single Denomination Combination](https://leetcode.com/problems/kth-smallest-amount-with-single-denomination-combination/)


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