# [3974. Maximum Total Sum of K Selected Elements](https://leetcode.com/problems/maximum-total-sum-of-k-selected-elements/description/)  

<code>Medium</code> level 

You are given an integer array <code>nums</code> and two integers <code>k</code> and <code>mul</code>.  

Select <strong>exactly</strong> <code>k</code> elements from <code>nums</code>. Process these elements one by one in any order you choose.

For each selected element, <strong>independently</strong> choose one of the following:

<li><strong>Add</strong> the element's value to the total sum, or</li>  
<li><strong>Multiply</strong> the element by the <strong>current</strong> value of <code>mul</code> and <strong>add</strong> the result to the total sum.</li>  
<br />
After processing each selected element, <code>mul</code> <strong>decreases</strong> by 1, regardless of which option was chosen. The current value of <code>mul</code> may become 0 or negative.  

<br />
Return an integer denoting the <strong>maximum</strong> possible total sum. 

<br />
<strong>Example 1:</strong>  
<pre>
<strong>Input:</strong> nums = [6,1,2,9], k = 3, mul = 2  
<strong>Output:</strong> 26  
</pre>

<strong>Explanation:</strong>  

One optimal way:  
<li>One optimal selection is <code>nums[3] = 9</code>, <code>nums[0] = 6</code>, and <code>nums[2] = 2</code>.</li>  
<li>Process <code>nums[3] = 9</code> first: choose multiplication, so it contributes <code>9 * 2 = 18</code>. Now, <code>mul</code> becomes 1.</li>
<li>Process <code>nums[0] = 6</code> next: choose multiplication, so it contributes <code>6 * 1 = 6</code>. Now, <code>mul</code> becomes 0.</li>
<li>Process <code>nums[2] = 2</code> last: choose addition, so it contributes 2.</li>
<li>The total sum is <code>18 + 6 + 2 = 26</code>.</li>

<br/>

<strong>Example 2:</strong>  
<pre>
<strong>Input:</strong> nums = [3,7,5,2], k = 2, mul = 4  
<strong>Output:</strong> 43  
</pre>

<strong>Explanation:</strong>  

One optimal way:
<li>One optimal selection is <code>nums[1] = 7</code> and <code>nums[2] = 5</code>.</li>
<li>Process <code>nums[1] = 7</code> first: choose multiplication, so it contributes <code>7 * 4 = 28</code>. Now, <code>mul</code> becomes 3.</li>
<li>Process <code>nums[2] = 5</code> next: choose multiplication, so it contributes <code>5 * 3 = 15</code>.</li>
<li>The total sum is <code>28 + 15 = 43</code>.</li>
<br/>

<strong>Example 3:</strong>  
<pre>
<strong>Input:</strong> nums = [4,4], k = 1, mul = 1  
<strong>Output:</strong> 4  
</pre>

<strong>Explanation:</strong>  

One optimal way:
<li>One optimal selection is <code>nums[0] = 4</code>.</li>
<li>Process <code>nums[0] = 4</code>: choose multiplication, so it contributes <code>4 * 1 = 4</code>.</li>
<li>The total sum is 4.</li>
<br/>

<strong>Constraints:</strong>

<li><code>1 <= nums.length <= 10<sup>5</sup></code></li>
<li><code>1 <= nums[i] <= 10<sup>5</sup></code></li>
<li><code>1 <= k <= nums.length</code></li>
<li><code>1 <= mul <= 10<sup>5</sup></code></li>  
<br />  

***

<h3>Solution</h3>  

<strong>Time complexity:</strong> <code>O(nlogn)</code>  
<strong>Space complexity:</strong> <code>O(log n)</code>

<strong>C++</strong>  

```C++
class Solution {
public:
    long long maximumTotalSum(vector<int>& nums, int k, int mul) {
      sort(nums.begin(), nums.end(), greater<int>());

      long long res = 0;

      for (int i = 0; i < k; i++) {
          long long currentMul = mul - i;

          long long coefficient = max(1LL, currentMul);

          res += 1LL * nums[i] * coefficient;
      }

      return res;
    }
};
```