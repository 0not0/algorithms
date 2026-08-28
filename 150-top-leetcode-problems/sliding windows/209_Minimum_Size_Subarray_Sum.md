# [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

**Medium** level

Given an array of positive integers <code>nums</code> and a positive integer <code>target</code>, return *the **minimal length** of a **subarray***<sup>1</sup> *whose sum is greater than or equal to* <code>target</code>. If there is no such subarray, return <code>0</code> instead.  

**1.** A **subarray** is a contiguous **non-empty** sequence of elements within an array.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> target = 7, nums = [2,3,1,2,4,3]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The subarray [4,3] has the minimal length under the problem constraint.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> target = 4, nums = [1,4,4]
<strong>Output:</strong> 1
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> target = 11, nums = [1,1,1,1,1,1,1,1]
<strong>Output:</strong> 0
</pre>

<br />

**Constraints:**

* <code>1 <= target <= 10<sup>9</sup></code>
* <code>1 <= nums.length <= 10<sup>5</sup></code>
* <code>1 <= nums[i] <= 10<sup>4</sup></code>  

<br />

**Follow up:** If you have figured out the <code>O(n)</code> solution, try coding another solution of which the time complexity is <code>O(n log(n))</code>.  

<br />

***  

**Solution**

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution 
{
  public:
    int minSubArrayLen(int target, vector<int>& nums)
    {
      int n = nums.size();
      long long sum = 0;
      int minLength = n + 1;

      for(int end = 0, start = 0; end < n; end++)
      {
        sum += nums[end];

        while(sum >= target)
        {
          minLength = min(minLength, end - start + 1);
          sum -= nums[start++];
        }
      }

      return minLength <= n ? minLength : 0;
    }
};
```

**JavaScript**
```JS
var minSubArrayLen = function(target, nums) {
  const n = nums.length;
  let sum = 0;
  let minLength = n + 1;

  for(let end = 0, start = 0; end < n; end++) {
    sum += nums[end];

    while(sum >= target) {
      minLength = Math.min(minLength, end - start + 1);
      sum -= nums[start++];
    }
  }

  return minLength <= n ? minLength : 0;
};
```