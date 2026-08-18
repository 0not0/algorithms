# [3471. Find the Largest Almost Missing Integer](https://leetcode.com/problems/find-the-largest-almost-missing-integer/)

You are given an integer array <code>nums</code> and an integer <code>k</code>.

An integer <code>x</code> is **almost missing** from <code>nums</code> if <code>x</code> appears in *exactly* one subarray of size <code>k</code> within <code>nums</code>.

Return the **largest almost missing** integer from <code>nums</code>. If no such integer exists, return <code>-1</code>.

A **subarray** is a contiguous sequence of elements within an array.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [3,9,2,1,7], k = 3
<strong>Output:</strong> 7
</pre>

**Explanation:**

* 1 appears in 2 subarrays of size 3: <code>[9, 2, 1]</code> and <code>[2, 1, 7]</code>.
* 2 appears in 3 subarrays of size 3: <code>[3, 9, 2]</code>, <code>[9, 2, 1]</code>, <code>[2, 1, 7]</code>.
* 3 appears in 1 subarray of size 3: <code>[3, 9, 2]</code>.
* 7 appears in 1 subarray of size 3: <code>[2, 1, 7]</code>.
* 9 appears in 2 subarrays of size 3: <code>[3, 9, 2]</code>, and <code>[9, 2, 1]</code>.  
  
We return 7 since it is the largest integer that appears in exactly one subarray of size <code>k</code>.

**Example 2:**
<pre>
<strong>Input:</strong> nums = [3,9,7,2,1,7], k = 4
<strong>Output:</strong> 3
</pre>

**Explanation:**

* 1 appears in 2 subarrays of size 4: <code>[9, 7, 2, 1]</code>, <code>[7, 2, 1, 7]</code>.
* 2 appears in 3 subarrays of size 4: <code>[3, 9, 7, 2]</code>, <code>[9, 7, 2, 1]</code>, <code>[7, 2, 1, 7]</code>.
* 3 appears in 1 subarray of size 4: <code>[3, 9, 7, 2]</code>.
* 7 appears in 3 subarrays of size 4: <code>[3, 9, 7, 2]</code>, <code>[9, 7, 2, 1]</code>, <code>[7, 2, 1, 7]</code>.
* 9 appears in 2 subarrays of size 4: <code>[3, 9, 7, 2]</code>, [<code>9, 7, 2, 1]</code>.

We return 3 since it is the largest and only integer that appears in exactly one subarray of size <code>k</code>.

**Example 3:**
<pre>
<strong>Input:</strong> nums = [0,0], k = 1
<strong>Output:</strong> -1
</pre>

**Explanation:**

There is no integer that appears in only one subarray of size 1.

<br />

**Constraints:**

* <code>1 <= nums.length <= 50</code>
* <code>0 <= nums[i] <= 50</code>
* <code>1 <= k <= nums.length</code>

<br />

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    int largestInteger(vector<int>& nums, int k)
    {
      int n = nums.size();
      int freq[51] = {};
      int ans = -1;

      if(k == n) 
        return *max_element(nums.begin(), nums.end());

      for(int x : nums)
        freq[x]++;

      if(k == 1)
      {
        for(int x = 50; x >= 0; x--)
        {
          if(freq[x] == 1) return x;
        }

        return -1;
      }

      if(freq[nums[0]] == 1)
        ans = nums[0];

      if(freq[nums[n - 1]] == 1)
        ans = max(ans, nums[n - 1]);

      return ans;
    }
};
```