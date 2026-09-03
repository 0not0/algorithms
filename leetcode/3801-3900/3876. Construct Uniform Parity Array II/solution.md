# [3876. Construct Uniform Parity Array II](https://leetcode.com/problems/construct-uniform-parity-array-ii) 

`Medium` level

You are given an array `nums1` of `n` **distinct** integers.

You want to construct another array `nums2` of length `n` such that the elements in `nums2` are either **all odd or all even**.

For each index `i`, you must choose **exactly one** of the following (in any order):

* `nums2[i] = nums1[i]​​​​​​​`
* `nums2[i] = nums1[i] - nums1[j]`, for an index `j != i`, such that `nums1[i] - nums1[j] >= 1`  

Return `true` if it is possible to construct such an array, otherwise return `false`.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums1 = [1,4,7]
<strong>Output:</strong> true
</pre>

**Explanation:​​​​​​​​​​​​​​**

* Set `nums2[0] = nums1[0] = 1`.
* Set `nums2[1] = nums1[1] - nums1[0] = 4 - 1 = 3`.
* Set `nums2[2] = nums1[2] = 7`.
* `nums2 = [1, 3, 7]`, and all elements are odd. Thus, the answer is `true`.

**Example 2:**
<pre>
<strong>Input:</strong> nums1 = [2,3]
<strong>Output:</strong> false
</pre>

**Explanation:**

It is not possible to construct `nums2` such that all elements have the same parity. Thus, the answer is `false`.

**Example 3:**
<pre>
<strong>Input:</strong> nums1 = [4,6]
<strong>Output:</strong> true
</pre>

**Explanation:**

* Set `nums2[0] = nums1[0] = 4`.
* Set `nums2[1] = nums1[1] = 6`.
* `nums2 = [4, 6]`, and all elements are even. Thus, the answer is `true`.

<br />

**Constraints:**

* <code>1 <= n == nums1.length <= 10<sup>5</sup></code>
* <code>1 <= nums1[i] <= 10<sup>9</sup></code>
* `nums1` consists of distinct integers.

<br />

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