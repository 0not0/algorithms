# [3568. Minimum Moves to Clean the Classroom](https://leetcode.com/problems/minimum-moves-to-clean-the-classroom)  

`Medium` level

<br />

***

### Solution

**Time complexity:**  <code>O(n)</code>  
**Space complexity:**  <code>O(n)</code>  

**C++**

```C++
class Solution {
public:
  int minMoves(vector<string>& classroom, int energy) {
    int m = classroom.size();
    int n = classroom[0].size();

    int startRow = 0;
    int startCol = 0;

    int litterCount = 0;
    vector<vector<int>> litterId(m, vector<int>(n, -1));

    for(int i = 0; i < m; i++)
    {
      for(int c = 0; c < n; c++) 
      {
        if(classroom[i][c] == 'S') 
        {
          startRow = i;
          startCol = c;
        } 
        else if(classroom[i][c] == 'L') 
        {
          litterId[i][c] = litterCount++;
        }
      }
    }

    int fullMask = (1 << litterCount) - 1;

    struct State {
      int row;
      int col;
      int mask;
      int energy;
    };

    queue<State> q;
    q.push({startRow, startCol, fullMask, energy});

    vector<vector<vector<int>>> bestEnergy(m, vector<vector<int>>(n, vector<int>(1 << litterCount, -1)));

    bestEnergy[startRow][startCol][fullMask] = energy;

    const int dirs[5] = {-1, 0, 1, 0, -1};

    int moves = 0;

    while(!q.empty()) 
    {
      int size = q.size();

      while(size--) 
      {
        auto [row, col, mask, currEnergy] = q.front();
        q.pop();

        if(mask == 0) return moves;

        if(currEnergy == 0) continue;

        for(int i = 0; i < 4; i++) {
          int nr = row + dirs[i];
          int nc = col + dirs[i + 1];

          if(nr < 0 || nr >= m || nc < 0 || nc >= n || classroom[nr][nc] == 'X') continue;

          int nextEnergy = currEnergy - 1;
          int nextMask = mask;

          if(classroom[nr][nc] == 'R') nextEnergy = energy;

          if(classroom[nr][nc] == 'L') nextMask &= ~(1 << litterId[nr][nc]);

          if(bestEnergy[nr][nc][nextMask] >= nextEnergy) continue;

          bestEnergy[nr][nc][nextMask] = nextEnergy;

          q.push({ nr, nc, nextMask, nextEnergy });
        }
      }

      moves++;
    }

      return -1;
    }
};
```