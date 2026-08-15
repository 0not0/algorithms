# [3702. Longest Subsequence With Non-Zero Bitwise XOR](https://leetcode.com/problems/longest-subsequence-with-non-zero-bitwise-xor/)

<code>Medium</code> level


***

### Solution  

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(1)</code>   

**C++**  
```C++
class Solution
{
  public:
    int longestSubsequence(vector<int>& nums)
    {
      int xr = 0;
      bool hasNonZero = false;

      for(int x : nums)
      {
        xr ^= x;
        if(x != 0) hasNonZero = true;
      }

      if(xr != 0) return nums.size();

      if(!hasNonZero) return 0; and 

      return nums.size() - 1;
    }
};
```