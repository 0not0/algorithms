# [3513. Number of Unique XOR Triplets I](https://leetcode.com/problems/number-of-unique-xor-triplets-i/)

<code>Medium</code> level 


***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  
**where:**
<code>q = queries.length</code>

**C++**

```C++
class Solution {
public:
  int uniqueXorTriplets(vector<int>& nums) {
    const auto n = nums.size();

    const auto& bit_length = [](int64_t x) {
      return (x ? __lg(x) : -1) + 1;
    };

    return n >= 3 ? 1 << bit_length(n) : n;
  }
};
```