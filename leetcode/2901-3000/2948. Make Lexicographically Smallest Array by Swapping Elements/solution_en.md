# [2948. Make Lexicographically Smallest Array by Swapping Elements](https://leetcode.com/problems/make-lexicographically-smallest-array-by-swapping-elements)  

<code>Medium</code> level  

You are given a **0-indexed** array of **positive** integers <code>nums</code> and a **positive** integer <code>limit</code>.

In one operation, you can choose any two indices <code>i</code> and <code>j</code> and swap <code>nums[i]</code> and <code>nums[j]</code> if <code>|nums[i] - nums[j]| <= limit</code>.

Return *the **lexicographically smallest array** that can be obtained by performing the operation any number of times*.

An array <code>a</code> is lexicographically smaller than an array <code>b</code> if in the first position where <code>a</code> and <code>b</code> differ, array <code>a</code> has an element that is less than the corresponding element in <code>b</code>. For example, the array <code>[2,10,3]</code> is lexicographically smaller than the array <code>[10,2,3]</code> because they differ at index <code>0</code> and <code>2 < 10</code>.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [1,5,3,9,8], limit = 2
<strong>Output:</strong> [1,3,5,8,9]
<strong>Explanation:</strong> Apply the operation 2 times:
- Swap nums[1] with nums[2]. The array becomes [1,3,5,9,8]
- Swap nums[3] with nums[4]. The array becomes [1,3,5,8,9]
We cannot obtain a lexicographically smaller array by applying any more operations.
Note that it may be possible to get the same result by doing different operations.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> nums = [1,7,6,18,2,1], limit = 3
<strong>Output:</strong> [1,6,7,18,1,2]
<strong>Explanation:</strong> Apply the operation 3 times:
- Swap nums[1] with nums[2]. The array becomes [1,6,7,18,2,1]
- Swap nums[0] with nums[4]. The array becomes [2,6,7,18,1,1]
- Swap nums[0] with nums[5]. The array becomes [1,6,7,18,1,2]
We cannot obtain a lexicographically smaller array by applying any more operations.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> nums = [1,7,28,19,10], limit = 3
<strong>Output:</strong> [1,7,28,19,10]
<strong>Explanation:</strong> [1,7,28,19,10] is the lexicographically smallest array we can obtain because we cannot apply the operation on any two indices.
</pre>  

<br />

**Constraints:**

* <code>1 <= nums.length <= 10<sup>5</sup></code>
* <code>1 <= nums[i] <= 10<sup>9</sup></code>
* <code>1 <= limit <= 10<sup>9</sup></code>  

<br />

***

### Solution  

**Time complexity:**  <code>O(n logn)</code>  
**Space complexity:**  <code>O(n)</code>   

**C++**  
```C++
class Solution
{
  public:
    vector<int> lexicographicallySmallestArray(vector<int>& nums, int limit)
    {
      int n = nums.size();

      vector<pair<int, int>> sorted(n);

      for(int i = 0; i < n; i++) sorted[i] = {nums[i], i};

      sort(sorted.begin(), sorted.end());

      vector<int> ans(n);
      vector<int> indices;
      indices.reserve(n);

      int left = 0;

      while(left < n)
      {
        int right = left;

        while(right + 1 < n && sorted[right + 1].first - sorted[right].first <= limit) right++;

        indices.clear();

        for(int i = left; i <= right; i++) indices.push_back(sorted[i].second);

        sort(indices.begin(), indices.end());

        for(int i = 0; i < indices.size(); i++) ans[indices[i]] = sorted[left + i].first;

        left = right + 1;
      }

      return ans;
    }
};
```