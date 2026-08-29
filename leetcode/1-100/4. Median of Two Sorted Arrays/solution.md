# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)  

<code>Hard</code> level  

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums1 = [1,3], nums2 = [2]
<strong>Output:</strong> 2.00000
<strong>Explanation:</strong> merged array = [1,2,3] and median is 2.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> nums1 = [1,2], nums2 = [3,4]
<strong>Output:</strong> 2.50000
<strong>Explanation:</strong> merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
</pre>

<br />

**Constraints:**

* <code>nums1.length == m</code>
* <code>nums2.length == n</code>
* <code>0 <= m <= 1000</code>
* <code>0 <= n <= 1000</code>
* <code>1 <= m + n <= 2000</code>
* <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code> 

