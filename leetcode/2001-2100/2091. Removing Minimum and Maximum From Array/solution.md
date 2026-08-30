# [2091. Removing Minimum and Maximum From Array](https://leetcode.com/problems/removing-minimum-and-maximum-from-array)  

`Medium` level  

You are given a **0-indexed** array of **distinct** integers `nums`.

There is an element in `nums` that has the **lowest** value and an element that has the **highest** value. We call them the **minimum** and **maximum** respectively. Your goal is to remove **both** these elements from the array.

A **deletion** is defined as either removing an element from the **front** of the array or removing an element from the **back** of the array.

Return *the **minimum** number of deletions it would take to remove **both** the minimum and maximum element from the array.*  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [2,<ins><b>10</b></ins>,7,5,4,<ins><b>1</b></ins>,8,6]
<strong>Output:</strong> 5
<strong>Explanation:</strong>
The minimum element in the array is nums[5], which is 1.
The maximum element in the array is nums[1], which is 10.
We can remove both the minimum and maximum by removing 2 elements from the front and 3 elements from the back.
This results in 2 + 3 = 5 deletions, which is the minimum number possible.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> nums = [0,<ins><b>-4</b></ins>,<ins><b>19</b></ins>,1,8,-2,-3,5]
<strong>Output:</strong> 3
<strong>Explanation:</strong> 
The minimum element in the array is nums[1], which is -4.
The maximum element in the array is nums[2], which is 19.
We can remove both the minimum and maximum by removing 3 elements from the front.
This results in only 3 deletions, which is the minimum number possible.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> nums = [<ins><b>101</b></ins>]
<strong>Output:</strong> 1
<strong>Explanation:</strong>
There is only one element in the array, which makes it both the minimum and maximum element.
We can remove it with 1 deletion.
</pre>

<br />

**Constraints:**

* <code>1 <= nums.length <= 10<sup>5</sup></code>
* <code>-10<sup>5</sup> <= nums[i] <= 10<sup>5</sup></code>
* The integers in `nums` are **distinct**.

<br />

***

**Solution**  

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>

**C++**  
```C++
class Solution
{
  public:
    int minimumDeletions(vector<int>& nums)
    {
      int n = nums.size();

      int minI = 0;
      int maxI = 0;

      for(int i = 1; i < n; i++)
      {
        if(nums[i] < nums[minI]) minI = i;
            
        if(nums[i] > nums[maxI]) maxI = i;      
      }

      int l = min(minI, maxI);
      int r = max(minI, maxI);

      int fromL = r + 1;
      int fromR = n - l;
      int both = (l + 1) + (n - r);

      return min({fromL, fromR, both});
    }
};
```