# [3871. Count Commas in Range II](https://leetcode.com/problems/count-commas-in-range-ii/)   

`Medium` level  

<br />

***

### Solution

**Time complexity:**  <code>O(log n)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```C++
class Solution {
public:
  long long countCommas(long long n) {
    long long result = 0;
    long long next = 1000;

    for(next; next <= n; next *= 1000) 
      result += n - next + 1;

    return result;
  }
};
```