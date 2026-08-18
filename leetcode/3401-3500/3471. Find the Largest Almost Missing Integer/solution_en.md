# [3471. Find the Largest Almost Missing Integer](https://leetcode.com/problems/find-the-largest-almost-missing-integer/)

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    int largestInteger(vector<int>& nums, int k)
    {
      int n = nums.size();
      int freq[51] = {};
      int ans = -1;

      if(k == n) 
        return *max_element(nums.begin(), nums.end());

      for(int x : nums)
        freq[x]++;

      if(k == 1)
      {
        for(int x = 50; x >= 0; x--)
        {
          if(freq[x] == 1) return x;
        }

        return -1;
      }

      if(freq[nums[0]] == 1)
        ans = nums[0];

      if(freq[nums[n - 1]] == 1)
        ans = max(ans, nums[n - 1]);

      return ans;
    }
};
```