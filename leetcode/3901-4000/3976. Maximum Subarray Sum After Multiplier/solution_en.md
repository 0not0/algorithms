# [3976. Maximum Subarray Sum After Multiplier](https://leetcode.com/problems/maximum-subarray-sum-after-multiplier/)  

<code>Medium</code> level  

You are given an integer array <code>nums</code> and a positive integer <code>k</code>.  
You must choose <strong>exactly</strong> one <strong>subarray</strong> of <code>nums</code> and perform <strong>exactly</strong> one of the following operations:  
1. Multiply each number in the chosen subarray by <code>k</code>.
2. Divide each number in the chosen subarray by <code>k</code>.
<li>When dividing a positive number by <code>k</code>, use the <strong>floor</strong> value of the division result.</li>
<li>When dividing a negative number by <code>k</code>, use the <strong>ceiling</strong> value of the division result.</li>
<br />
Return the <strong>maximum</strong> possible sum of a <strong>non-empty</strong> subarray in the resulting array.  

Note that the subarray chosen for the operation and the subarray chosen for the sum may be <strong>different</strong>.  
<br />
<strong>Example 1:</strong>  
<pre>
<strong>Input:</strong> nums = [1,-2,3,4,-5], k = 2  
<strong>Output:</strong> 14  
</pre>
<strong>Explanation:</strong>  

<li>Multiply each number in the subarray <code>[3, 4]</code> by 2.</li>
<li>This results in <code>nums = [1, -2, 6, 8, -5]</code>.</li>
<li>The subarray with the largest sum is <code>[6, 8]</code>, so the output is <code>6 + 8 = 14</code>.</li>  
<br/>
<strong>Example 2:</strong>
<br />
<pre>
<strong>Input</strong>: nums = [-5,-4,-3], k = 2  
<strong>Output</strong>: -1
</pre>  

<strong>Explanation:</strong>  
<li>Divide each number in the subarray <code>[-3]</code> by 2.</li>
<li>This results in <code>nums = [-5, -4, -1]</code>.</li>
<li>The subarray with the largest sum is <code>[-1]</code>, so the output is -1.</li>  
<br />
<strong>Constraints:</strong>

<li><code>1 <= nums.length <= 10<sup>5</sup></code></li>
<li><code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code></li>
<li><code>1 <= k <= 10<sup>5</sup></code></li>   

***


<h3>Solution</h3>  

<strong>Time complexity:</strong> <code>O(n)</code>  
<strong>Space complexity:</strong> <code>O(1)</code>

<strong>C++</strong>  

```C++
#include <vector>
#include <algorithm>

class Solution {
public:
    long long maxSubarraySum(std::vector<int>& nums, int k) {
      return std::max(solve(nums, k, true), solve(nums, k, false));
    }

private:
  long long solve(std::vector<int>& nums, int k, bool multiply) {
    const long long NEG = -4e18;

    long long dp0 = NEG;
    long long dp1 = NEG;
    long long dp2 = NEG;

    long long ans = NEG;

    for (int x : nums) {
      long long val = multiply ? 1LL * x * k : x / k;

      long long ndp0 = std::max((long long)x, dp0 + x);

      long long ndp1 = std::max({val, dp0 + val, dp1 + val});

      long long ndp2 = std::max(dp1 + x, dp2 + x);

      dp0 = ndp0;
      dp1 = ndp1;
      dp2 = ndp2;

      ans = std::max({ans, dp0, dp1, dp2});
    }

    return ans;
  }
};
```
