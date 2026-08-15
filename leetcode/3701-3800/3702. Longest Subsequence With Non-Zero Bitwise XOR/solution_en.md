# [3702. Longest Subsequence With Non-Zero Bitwise XOR](https://leetcode.com/problems/longest-subsequence-with-non-zero-bitwise-xor/)

<code>Medium</code> level

You are given an integer array <code>nums</code>.

Return the length of the **longest** **subsequence**<sup>1</sup> in <code>nums</code> whose bitwise **XOR** is **non-zero**. If no such **subsequence** exists, return 0.

**1.** A **subsequence** is an **non-empty** array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

<br />

**Example 1:**
<pre>
Input: nums = [1,2,3]
Output: 2
</pre>

**Explanation:**

One longest subsequence is <code>[2, 3]</code>. The bitwise XOR is computed as <code>2 XOR 3 = 1</code>, which is non-zero.

**Example 2:**
<pre>
Input: nums = [2,3,4]
Output: 3
</pre>

**Explanation:**

The longest subsequence is <code>[2, 3, 4]</code>. The bitwise XOR is computed as <code>2 XOR 3 XOR 4 = 5</code>, which is non-zero.  

<br />

**Constraints:**

* <code>1 <= nums.length <= 10<sup>5</sup></code>
* <code>0 <= nums[i] <= 10<sup>9</sup></code>

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
    int longestSubsequence(vector<int>& nums)
    {
      int xr = 0;
      bool hasNonZero = false;

      for(int x : nums)
      {
        xr ^= x;
        if(x != 0) hasNonZero = true;
      }

      if(xr != 0) return nums.size();

      if(!hasNonZero) return 0; and 

      return nums.size() - 1;
    }
};
```