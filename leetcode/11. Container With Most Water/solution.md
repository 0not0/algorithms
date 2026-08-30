# [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water)  

`Medium` level  

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the <code>i<sup>th</sup></code> line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container. 

<br />

**Example 1:**  
![11 problem example one image](/images/problems/11/11-problems-example-1.png)  
<pre>
<strong>Input:</strong> height = [1,8,6,2,5,4,8,3,7]
<strong>Output:</strong> 49
<strong>Explanation:</strong> The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.  
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> height = [1,1]
<strong>Output:</strong> 1
</pre>

<br />

**Constraints:**

* <code>n == height.length</code>
* <code>2 <= n <= 10<sup>5</sup></code>
* <code>0 <= height[i] <= 10<sup>4</sup></code>

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
    int maxArea(vector<int>& height)
    {
      int left = 0;
      int right = height.size() - 1;
      int ans = 0;

      while(left < right)
      {
        int h = min(height[left], height[right]);

        ans = max(ans, h * (right - left));

        while (left < right && height[left] <= h) left++;
          
        while (left < right && height[right] <= h) right--;

      }

      return ans;
    }
};
```