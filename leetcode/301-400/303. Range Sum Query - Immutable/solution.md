# [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/)  

`Easy` level  

Given an integer array `nums`, handle multiple queries of the following type:

1\. Calculate the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** where `left <= right`.  

Implement the `NumArray` class:

* `NumArray(int[] nums)` Initializes the object with the integer array `nums`.
* `int sumRange(int left, int right)` Returns the **sum** of the elements of `nums` between indices `left` and `right` **inclusive** (i.e. `nums[left] + nums[left + 1] + ... + nums[right]`).

<br />

**Example 1:**
<pre>
<strong>Input</strong>
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
<strong>Output</strong>
[null, 1, -1, -3]

<strong>Explanation</strong>
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return (-2) + 0 + 3 = 1
numArray.sumRange(2, 5); // return 3 + (-5) + 2 + (-1) = -1
numArray.sumRange(0, 5); // return (-2) + 0 + 3 + (-5) + 2 + (-1) = -3
</pre>

<br />

**Constraints:**

* <code>1 <= nums.length <= 10<sup>4</sup></code>
* <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>
* `0 <= left <= right < nums.length`
* At most <code>10<sup>4</sup></code> calls will be made to `sumRange`.

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