**Task:**  

### [3718. Smallest Missing Multiple of K](https://leetcode.com/problems/smallest-missing-multiple-of-k)

<code>Easy</code> level  
Three solutions with different runtimes.

**First solution**  

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code> 
```C++
class Solution 
{
  public:
    int missingMultiple(vector<int>& nums, int k)
    {
      bool present[101] = {};

      for(int x : nums) present[x] = true;

      for(int x = k; x <= 100; x += k)
      {
        if (!present[x]) return x;
      }

      return ((100 / k) + 1) * k;
    }
};
```

**Second solution**

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(n)</code> 
```C++
class Solution 
{
  public:
    int missingMultiple(vector<int>& nums, int k) 
    {
      unordered_set<int> seen(nums.begin(), nums.end());

      for(int x = k; ; x += k)
        if (!seen.contains(x)) return x;
    }
};
```

**Third solution**

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code> 
```C++
class Solution
{
  public:
    int missingMultiple(vector<int>& nums, int k)
    {
      for(int x = k; ; x += k) 
      {
        bool found = false;

        for(int num : nums) 
        {
          if(num == x) 
          {
            found = true;
            break;
          }
        }

        if(!found) return x;
      }
    }
};
```