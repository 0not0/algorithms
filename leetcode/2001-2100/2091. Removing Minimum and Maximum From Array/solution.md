# [2091. Removing Minimum and Maximum From Array](https://leetcode.com/problems/removing-minimum-and-maximum-from-array)  

<code>Medium</code> level  

***

**Solution**  

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>

**C++**  
```C++
class Solution
{
  public:
    int minimumDeletions(vector<int>& nums)
    {
      int n = nums.size();

      int minI = 0;
      int maxI = 0;

      for(int i = 1; i < n; i++)
      {
        if(nums[i] < nums[minI]) minI = i;
            
        if(nums[i] > nums[maxI]) maxI = i;      
      }

      int l = min(minI, maxI);
      int r = max(minI, maxI);

      int fromL = r + 1;
      int fromR = n - l;
      int both = (l + 1) + (n - r);

      return min({fromL, fromR, both});
    }
};
```