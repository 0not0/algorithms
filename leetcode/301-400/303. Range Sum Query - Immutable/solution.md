# [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/)  

`Easy` level  



<br />

***

### Solution

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(n)</code>  

**C++**

```C++
class NumArray {
private:
  vector<int> prefix;

public:
  NumArray(vector<int>& nums)
  {
    prefix.resize(nums.size() + 1);

    for(int i = 0; i < nums.size(); i++)
    {
        prefix[i + 1] = prefix[i] + nums[i];
    }
  }
  
  int sumRange(int left, int right)
  {
    return prefix[right + 1] - prefix[left];
  }
};
```