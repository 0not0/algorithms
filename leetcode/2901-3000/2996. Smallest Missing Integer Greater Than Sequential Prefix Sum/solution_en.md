# [2996. Smallest Missing Integer Greater Than Sequential Prefix Sum](https://leetcode.com/problems/smallest-missing-integer-greater-than-sequential-prefix-sum/)

<code>Easy</code> level 

You are given a **0-indexed** array of integers <code>nums</code>.

A prefix <code>nums[0..i]</code> is **sequential** if, for all <code>1 <= j <= i, nums[j] = nums[j - 1] + 1</code>. In particular, the prefix consisting only of <code>nums[0]</code> is **sequential**.

Return *the **smallest** integer* <code>x</code> *missing from* <code>nums</code> *such that* <code>x</code> *is greater than or equal to the sum of the **longest** sequential prefix*.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [1,2,3,2,5]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The longest sequential prefix of nums is [1,2,3] with a sum of 6. 6 is not in the array, therefore 6 is the smallest missing integer greater than or equal to the sum of the longest sequential prefix. 
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> nums = [3,4,5,1,12,14,13]
<strong>Output:</strong> 15
<strong>Explanation:</strong> The longest sequential prefix of nums is [3,4,5] with a sum of 12. 12, 13, and 14 belong to the array while 15 does not. Therefore 15 is the smallest missing integer greater than or equal to the sum of the longest sequential prefix.  
</pre>

<br />

**Constraints:**

* <code>1 <= nums.length <= 50</code>
* <code>1 <= nums[i] <= 50</code>  

<br />

***

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>   

**C++**  
```C++
class Solution 
{
  public:
    int missingInteger(vector<int>& nums)
    {
      bool present[51] = {};

      for(int x : nums)
      {
        present[x] = true;
      }

      int sum = nums[0];

      for(int i = 1; i < nums.size() && nums[i] == nums[i - 1] + 1; i++)
      {
        sum += nums[i];
      }

      while(sum <= 50 && present[sum])
      {
        sum++;
      }

      return sum;
  }
};
```