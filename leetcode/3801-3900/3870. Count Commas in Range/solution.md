# [3870. Count Commas in Range](https://leetcode.com/problems/count-commas-in-range/)

`Easy` level  

<br />

***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```C++
class Solution {
public:
  int countCommas(int n)
  {
    return max(0, n - 999);
  }
};
```