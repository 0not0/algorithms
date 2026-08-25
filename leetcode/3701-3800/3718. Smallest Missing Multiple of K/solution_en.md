# [3718. Smallest Missing Multiple of K]()

<code>Easy</code> level  

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    int missingMultiple(vector<int>& nums, int k)
    {
      bool seen[101] = {};

      for(int x : nums) seen[x] = true;

      for(int x = k; x <= 100; x += k)
        if (!seen[x]) return x;

      return (100 / k + 1) * k;
    }
};
```