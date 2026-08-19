# [1386. Cinema Seat Allocation](https://leetcode.com/problems/cinema-seat-allocation/)


***  

### Solution

**Time complexity:** <code>O(m)</code>  
**Space complexity:** <code>O(m)</code>  

**C++**
```C++
class Solution 
{
  public:
    int maxNumberOfFamilies(int n, vector<vector<int>>& reservedSeats)
    {
      const int LEFT   = 0b00001111;
      const int MIDDLE = 0b00111100;
      const int RIGHT  = 0b11110000;
      unordered_map<int, int> rowMask;

      for(auto& seat : reservedSeats)
      {
        int row = seat[0];
        int col = seat[1];

        if(col >= 2 && col <= 9) rowMask[row] |= 1 << (col - 2);
      }

      int ans = 2 * (n - rowMask.size());

      for(auto& [row, mask] : rowMask)
      {
        bool leftFree  = !(mask & LEFT);
        bool rightFree = !(mask & RIGHT);

        if(leftFree && rightFree) ans += 2;
        else if(leftFree || rightFree || !(mask & MIDDLE)) ans += 1;
      }

      return ans;
    }
};
```