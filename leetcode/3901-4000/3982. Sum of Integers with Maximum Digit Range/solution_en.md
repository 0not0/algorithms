# [3982. Sum of Integers with Maximum Digit Range](https://leetcode.com/problems/sum-of-integers-with-maximum-digit-range/)  

<code>Easy</code> level 

You are given an integer array <code>nums</code>.

The **digit range** of an integer is defined as the difference between its **largest** digit and **smallest** digit.

For example, the digit range of 5724 is <code>7 - 2 = 5</code>.

Return the sum of all integers in <code>nums</code> whose **digit range** is equal to the **maximum digit range** among all integers in the array.  

**Example 1:**
<pre>
<strong>Input:</strong> nums = [5724,111,350]
<strong>Output:</strong> 6074
</pre>
**Explanation:**  

|<code>i</code> | <code>nums[i]</code>| Largest | Smallest | Digit Range |      
| :------:      |    :---------: | :--:  | :----: | :-----:  |
|0| 5724 | 7 | 2 | 5 |
|1| 111  | 1 | 1 | 0 |
|2| 350  | 5 | 0 | 5 |

The maximum digit range is 5. The integers with this digit range are 5724 and 350, so the answer is <code>5724 + 350 = 6074</code>.

**Example 2:**
<pre>
<strong>Input:</strong> nums = [90,900]
<strong>Output:</strong> 990
</pre>
**Explanation:**
|<code>i</code> | <code>nums[i]</code>| Largest | Smallest | Digit Range |      
| :------:      |    :---------: | :--:  | :----: | :-----:  |
|0| 90 | 9 | 0 | 9 |
|1| 900  | 9 | 0 | 9 |

The maximum digit range is 9. Both integers have this digit range, so the answer is <code>90 + 900 = 990</code>.

**Constraints:**

+ <code>1 <= nums.length <= 100</code>
+ <code>10 <= nums[i] <= 10<sup>5</sup></code> 

<br />

***  

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**
```C++
class Solution {
public:
    int maxDigitRange(vector<int>& nums) {
      int mx = 0;
      int ans = 0;
        
      for (int x : nums) {
        int a = 10;
        int b = 0;

        for (int y = x; y > 0; y /= 10) {
          int c = y % 10;

          a = min(a, c);
          b = max(b, c);
        }

      int d = b - a;

      if (mx < d) {
        mx = d;
        ans = x;
      } else if (mx == d) {
        ans += x;
      }
    }

    return ans;
  }
};
```
