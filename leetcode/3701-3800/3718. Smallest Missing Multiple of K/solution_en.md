# [3718. Smallest Missing Multiple of K]()

<code>Easy</code> level  

Given an integer array <code>nums</code> and an integer <code>k</code>, return the **smallest positive multiple** of <code>k</code> that is **missing** from <code>nums</code>.

A **multiple** of <code>k</code> is any positive integer divisible by <code>k</code>.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [8,2,3,4,6], k = 2
<strong>Output:</strong> 10
</pre>
**Explanation:**

The multiples of <code>k = 2</code> are 2, 4, 6, 8, 10, 12... and the smallest multiple missing from <code>nums</code> is 10.

**Example 2:**
<pre>
<strong>Input:</strong> nums = [1,4,7,10,15], k = 5
<strong>Output:</strong> 5
</pre>
**Explanation:**

The multiples of <code>k = 5</code> are 5, 10, 15, 20... and the smallest multiple missing from <code>nums</code> is 5.

<br />

**Constraints:**

* <code>1 <= nums.length <= 100</code>
* <code>1 <= nums[i] <= 100</code>
* <code>1 <= k <= 100</code>

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
    int missingMultiple(vector<int>& nums, int k)
    {
      bool seen[101] = {};

      for(int x : nums) seen[x] = true;

      for(int x = k; x <= 100; x += k)
        if (!seen[x]) return x;

      return (100 / k + 1) * k;
    }
};
```