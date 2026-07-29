# [3513. Number of Unique XOR Triplets I](https://leetcode.com/problems/number-of-unique-xor-triplets-i/)

<code>Medium</code> level 

You are given an integer array <code>nums</code> of length <code>n</code>, where nums is a **permutation** of the numbers in the range <code>[1, n]</code>.

A **XOR triplet** is defined as the XOR of three elements <code>nums[i] XOR nums[j] XOR nums[k]</code> where <code>i <= j <= k</code>.

Return the number of **unique** XOR triplet values from all possible triplets <code>(i, j, k)</code>.  

**Example 1:**
<pre>
<strong>Input:</strong> nums = [1,2]
<strong>Output:</strong> 2
</pre>
**Explanation:**

The possible XOR triplet values are:

* <code>(0, 0, 0) → 1 XOR 1 XOR 1 = 1</code>
* <code>(0, 0, 1) → 1 XOR 1 XOR 2 = 2</code>
* <code>(0, 1, 1) → 1 XOR 2 XOR 2 = 1</code>
* <code>(1, 1, 1) → 2 XOR 2 XOR 2 = 2</code>  
  
The unique XOR values are <code>{1, 2}</code>, so the output is 2.  

**Example 2:**
<pre>
<strong>Input:</strong> nums = [3,1,2]
<strong>Output:</strong> 4
</pre>
**Explanation:**

The possible XOR triplet values include:

* <code>(0, 0, 0) → 3 XOR 3 XOR 3 = 3</code>
* <code>(0, 0, 1) → 3 XOR 3 XOR 1 = 1</code>
* <code>(0, 0, 2) → 3 XOR 3 XOR 2 = 2</code>
* <code>(0, 1, 2) → 3 XOR 1 XOR 2 = 0</code>  

The unique XOR values are <code>{0, 1, 2, 3}</code>, so the output is 4.

**Constraints:**

* <code>1 <= n == nums.length <= 10<sup>5</sup></code>
* <code>1 <= nums[i] <= n</code>
* <code>nums</code> is a permutation of integers from <code>1</code> to <code>n</code>.

***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  
**where:**
<code>q = queries.length</code>  

**C++**

```C++
class Solution {
public:
  int uniqueXorTriplets(vector<int>& nums) {
    const auto n = nums.size();

    const auto& bit_length = [](int64_t x) {
      return (x ? __lg(x) : -1) + 1;
    };

    return n >= 3 ? 1 << bit_length(n) : n;
  }
};
```