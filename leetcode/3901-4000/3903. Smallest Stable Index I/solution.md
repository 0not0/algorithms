# [3903. Smallest Stable Index I](https://leetcode.com/problems/smallest-stable-index-i)  

`Easy` level  

You are given an integer array `nums` of length `n` and an integer `k`.

For each index `i`, define its **instability score** as `max(nums[0..i]) - min(nums[i..n - 1])`.

In other words:

* `max(nums[0..i])` is the **largest** value among the elements from index 0 to index `i`.
* `min(nums[i..n - 1])` is the **smallest** value among the elements from index `i` to index `n - 1`.
  
An index `i` is called **stable** if its instability score is **less than or equal to** `k`.

Return the **smallest** stable index. If no such index exists, return -1. 

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [5,0,1,4], k = 3
<strong>Output:</strong> 3
</pre>

**Explanation:**

* At index 0: The maximum in `[5]` is 5, and the minimum in `[5, 0, 1, 4]` is 0, so the instability score is `5 - 0 = 5`.
* At index 1: The maximum in `[5, 0]` is 5, and the minimum in `[0, 1, 4]` is 0, so the instability score is `5 - 0 = 5`.
* At index 2: The maximum in `[5, 0, 1]` is 5, and the minimum in `[1, 4]` is 1, so the instability score is `5 - 1 = 4`.
* At index 3: The maximum in `[5, 0, 1, 4]` is 5, and the minimum in `[4]` is 4, so the instability score is `5 - 4 = 1`.
* This is the first index with an instability score less than or equal to `k = 3`. Thus, the answer is 3.

**Example 2:**
<pre>
<strong>Input:</strong> nums = [3,2,1], k = 1
<strong>Output:</strong> -1
</pre>

**Explanation:**

* At index 0, the instability score is `3 - 1 = 2`.
* At index 1, the instability score is `3 - 1 = 2`.
* At index 2, the instability score is `3 - 1 = 2`.
* None of these values is less than or equal to `k = 1`, so the answer is -1.

**Example 3:**
<pre>
<strong>Input:</strong> nums = [0], k = 0
<strong>Output:</strong> 0
</pre>

**Explanation:**

At index 0, the instability score is `0 - 0 = 0`, which is less than or equal to `k = 0`. Therefore, the answer is 0.

<br />

**Constraints:**

* <code>1 <= nums.length <= 100</code>
* <code>0 <= nums[i] <= 10<sup>9</sup></code>
* <code>0 <= k <= 10<sup>9</sup></code>

<br />

***

### Solution

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(n)</code>  

**C++**

```C++
class Solution {
public:
    int firstStableIndex(vector<int>& nums, int k) {
      int n = nums.size();

      vector<int> suffixMin(n);
      suffixMin[n - 1] = nums[n - 1];

      for(int i = n - 2; i >= 0; i--) suffixMin[i] = min(nums[i], suffixMin[i + 1]);

      int prefixMax = nums[0];

      for(int i = 0; i < n; i++)
      {
        prefixMax = max(prefixMax, nums[i]);

        if(prefixMax - suffixMin[i] <= k) return i;           
      }

      return -1;
  }
};
```