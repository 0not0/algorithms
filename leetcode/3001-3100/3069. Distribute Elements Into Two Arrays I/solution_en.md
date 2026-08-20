# [3069. Distribute Elements Into Two Arrays I](https://leetcode.com/problems/distribute-elements-into-two-arrays-i/)

<code>Easy</code> level


***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(n)</code>  

**C++**
```C++
class Solution
{
  public:
    vector<int> resultArray(vector<int>& nums)
    {
      int n = nums.size();

      vector<int> arr1;
      vector<int> arr2;

      arr1.reserve(n);
      arr2.reserve(n);

      arr1.push_back(nums[0]);
      arr2.push_back(nums[1]);

      for(int i = 2; i < n; i++)
      {
        if(arr1.back() > arr2.back()) 
          arr1.push_back(nums[i]);
        else 
          arr2.push_back(nums[i]);
      }

      arr1.insert(arr1.end(), arr2.begin(), arr2.end());

      return arr1;
    }
};
```