# [3069. Distribute Elements Into Two Arrays I](https://leetcode.com/problems/distribute-elements-into-two-arrays-i/)

<code>Easy</code> level

You are given a **1-indexed** array of **distinct** integers <code>nums</code> of length <code>n</code>.

You need to distribute all the elements of <code>nums</code> between two arrays <code>arr1</code> and <code>arr2</code> using <code>n</code> operations. In the first operation, append <code>nums[1]</code> to <code>arr1</code>. In the second operation, append <code>nums[2]</code> to <code>arr2</code>. Afterwards, in the <code>i<sup>th</sup></code> operation:

* If the last element of <code>arr1</code> is **greater** than the last element of <code>arr2</code>, append <code>nums[i]</code> to <code>arr1</code>. Otherwise, append <code>nums[i]</code> to <code>arr2</code>.  

The array <code>result</code> is formed by concatenating the arrays <code>arr1</code> and <code>arr2</code>. For example, if <code>arr1 == [1,2,3]</code> and <code>arr2 == [4,5,6]</code>, then <code>result = [1,2,3,4,5,6]</code>.

Return *the array* <code>result</code>.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [2,1,3]
<strong>Output:</strong> [2,3,1]
</pre>

**Explanation:** After the first 2 operations, arr1 = [2] and arr2 = [1].
In the 3<sup>rd</sup> operation, as the last element of arr1 is greater than the last element of arr2 (2 > 1), append nums[3] to arr1.  
After 3 operations, arr1 = [2,3] and arr2 = [1].  
Hence, the array result formed by concatenation is [2,3,1].    

**Example 2:**
<pre>
<strong>Input:</strong> nums = [5,4,3,8]
<strong>Output:</strong> [5,3,4,8]
</pre>
**Explanation:** After the first 2 operations, arr1 = [5] and arr2 = [4].
In the 3<sup>rd</sup> operation, as the last element of arr1 is greater than the last element of arr2 (5 > 4), append nums[3] to arr1, hence arr1 becomes [5,3].
In the 4<sup>th</sup> operation, as the last element of arr2 is greater than the last element of arr1 (4 > 3), append nums[4] to arr2, hence arr2 becomes [4,8].  
After 4 operations, arr1 = [5,3] and arr2 = [4,8].  
Hence, the array result formed by concatenation is [5,3,4,8].  

<br />

**Constraints:**

* <code>3 <= n <= 50</code>
* <code>1 <= nums[i] <= 100</code>
* All elements in <code>nums</code> are distinct.

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
    vector<int> resultArray(vector<int>& nums)
    {
      int n = nums.size();

      vector<int> arr1;
      vector<int> arr2;

      arr1.reserve(n);
      arr2.reserve(n);

      arr1.push_back(nums[0]);
      arr2.push_back(nums[1]);

      for(int i = 2; i < n; i++)
      {
        if(arr1.back() > arr2.back()) 
          arr1.push_back(nums[i]);
        else 
          arr2.push_back(nums[i]);
      }

      arr1.insert(arr1.end(), arr2.begin(), arr2.end());

      return arr1;
    }
};
```