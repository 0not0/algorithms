# [1. Two Sum](https://leetcode.com/problems/two-sum/description/)  

<code>Easy</code> level

Given an array of integers <code>nums</code> and an integer <code>target</code>, return <em>indices of the two numbers such that they add up to <code>target</code></em>.  
You may assume that each input would have <strong><em>exactly</em> one solution</strong>, and you may not use the same element twice.   
You can return the answer in any order.

<strong>Example 1:</strong>  
<pre>
<strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
<strong>Explanation:</strong> Because nums[0] + nums[1] == 9, we return [0, 1].
</pre>  

<strong>Example 2:</strong>  
<pre>
<strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
</pre>  

<strong>Example 3:</strong>  
<pre>
<strong>Input:</strong> nums = [3,3], target = 6
<strong>Output:</strong> [0,1]
</pre>  

<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
	<li><strong>Only one valid answer exists.</strong></li>
</ul>  

<strong>Follow-up:</strong> Can you come up with an algorithm that is less than <code>O(n<sup>2</sup>)</code> time complexity?

***  

Розв'язування  

<strong>Два цикла <code>for</code></strong>  
Рішення, гарне по Space complexity, але погане по Time complexety.  
Space complexity: O(1)  
Time complexity: O(n<sup>2</sup>)  

#### JavaScript
```js
const twoSum = (nums, target) => {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
}
```  

Використання <strong>Hash Map</strong>.  
Покращує Time complexity, але погіршує Space complexity:   
Space complexity: O(n)  
Time complexity: O(n)
#### JavaScript

```js
const twoSum = (nums, target) => {
  const obj = {};

  for(let i = 0; i < nums.length; i++) {
      let val = target - nums[i];

      if(val in obj) {
          return [obj[val], i];
      } else {
          obj[nums[i]] = i;
      }
  }
}
```  
#### C++
```C++
class Solution {
public:
  vector<int> twoSum(vector<int>& nums, int target) {
    std::unordered_map<int, int> map;
  
    for (int i = 0; i < nums.size(); i++) {
      int val = target - nums.at(i);
          
      auto it = map.find(val);
          
      if (it != map.end()) {
          return {it->second, i};
      } else {
          map[nums[i]] = i;
      }
    }
    
    return {};
  }
};
```  