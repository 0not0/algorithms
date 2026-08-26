# [3985. Palindromic Subarray Sum](https://leetcode.com/problems/palindromic-subarray-sum/)  

<code>Hard</code> level 

You are given an integer array <code>nums</code>.

Return the maximum possible sum of a **subarray** of <code>nums</code> that is a **palindrome**.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [10,10]  
<strong>Output:</strong> 20
</pre>
**Explanation:**

The whole array <code>[10,10]</code> is a palindrome. Therefore, the maximum sum is <code>10 + 10 = 20</code>.  

<br />

**Example 2:**
<pre>
<strong>Input:</strong> nums = [1,2,3,2,1,5,6]
<strong>Output:</strong> 9
</pre>
**Explanation:**

The contiguous subarray <code>[1,2,3,2,1]</code> is a palindrome. Its sum is <code>1 + 2 + 3 + 2 + 1 = 9</code> and it is the maximum sum.  

<br />

**Example 3:**
<pre>
<strong>Input:</strong> nums = [7,1,2,1,7,3,4,3,4]
<strong>Output:</strong> 18
</pre>
**Explanation:**

The contiguous subarray <code>[7,1,2,1,7]</code> is a palindrome. Its sum is <code>7 + 1 + 2 + 1 + 7 = 18</code> and it is the maximum sum.  

<br />

**Example 4:**
<pre>
<strong>Input:</strong> nums = [1,2,3,4,5]
<strong>Output:</strong> 5
</pre>
**Explanation:**

No subarray with length greater than 1 is a palindrome. The largest element in the array is 5. Therefore, the answer is 5.

<br />

**Example 5:**
<pre>
<strong>Input:</strong> nums = [1000]
<strong>Output:</strong> 1000
</pre>
**Explanation:**

The subarray with only one element is a palindrome. Therefore, the answer is 1000.  

<br />

**Constraints:**

* <code>1 <= nums.length <= 10<sup>5</sup></code>
* <code>1 <= nums[i] <= 10​​​​​​<sup>​9</sup></code>

<br />

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(n)</code>  

**C++**
```C++
class Solution 
{
  public:
    long long getSum(vector<int>& nums)
    {
      int n = nums.size();
      vector<long long> prefix(n + 1);

      for(int i = 0; i < n; i++) prefix[i + 1] = prefix[i] + nums[i];

      auto rangeSum = [&](int l, int r)
      {
        return prefix[r + 1] - prefix[l];
      };

      long long ans = 0;

      vector<int> odd(n);

      for(int i = 0, l = 0, r = -1; i < n; i++)
      {
        int k = i > r ? 1 : min(odd[l + r - i], r - i + 1);

        while(i - k >= 0 && i + k < n && nums[i - k] == nums[i + k]) k++;

        odd[i] = k;
        ans = max(ans, rangeSum(i - k + 1, i + k - 1));

        if(i + k - 1 > r)
        {
          l = i - k + 1;
          r = i + k - 1;
        }
      }

      vector<int> even(n);

      for(int i = 0, l = 0, r = -1; i < n; i++)
      {
        int k = i > r ? 0 : min(even[l + r - i + 1], r - i + 1);

        while(i - k - 1 >= 0 && i + k < n && nums[i - k - 1] == nums[i + k]) k++;

        even[i] = k;

        if(k > 0) ans = max(ans, rangeSum(i - k, i + k - 1));

        if(i + k - 1 > r)
        {
          l = i - k;
          r = i + k - 1;
        }
      }

      return ans;
    }
};
```