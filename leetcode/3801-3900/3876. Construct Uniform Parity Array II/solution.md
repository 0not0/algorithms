# [3876. Construct Uniform Parity Array II](https://leetcode.com/problems/construct-uniform-parity-array-ii) 

`Medium` level

***

### Solution

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```C++
class Solution {
public:
    bool uniformArray(vector<int>& nums1) {
      int minValue = *min_element(nums1.begin(), nums1.end());

      if(minValue % 2 == 1) return true;

      for(int x : nums1)
      {
        if(x % 2 == 1) return false;
      }

      return true;
    }
};
```