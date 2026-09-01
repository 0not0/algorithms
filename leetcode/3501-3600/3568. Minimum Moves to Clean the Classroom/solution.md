# [3568. Minimum Moves to Clean the Classroom](https://leetcode.com/problems/minimum-moves-to-clean-the-classroom)  

`Medium` level

You are given an `m x n` grid `classroom` where a student volunteer is tasked with cleaning up litter scattered around the room. Each cell in the grid is one of the following:

* `'S'`: Starting position of the student
* `'L'`: Litter that must be collected (once collected, the cell becomes empty)
* `'R'`: Reset area that restores the student's energy to full capacity, regardless of their current energy level (can be used multiple times)
* `'X'`: Obstacle the student cannot pass through
* `'.'`: Empty space  

You are also given an integer `energy`, representing the student's maximum energy capacity. The student starts with this energy from the starting position `'S'`.

Each move to an adjacent cell (up, down, left, or right) costs 1 unit of energy. If the energy reaches 0, the student can only continue if they are on a reset area `'R'`, which resets the energy to its **maximum** capacity `energy`.

Return the **minimum** number of moves required to collect all litter items, or `-1` if it's impossible.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> classroom = ["S.", "XL"], energy = 2
<strong>Output:</strong> 2
</pre>

**Explanation:**

* The student starts at cell `(0, 0)` with 2 units of energy.
* Since cell `(1, 0)` contains an obstacle 'X', the student cannot move directly downward.
* A valid sequence of moves to collect all litter is as follows:
  * Move 1: From `(0, 0)` → `(0, 1)` with 1 unit of energy and 1 unit remaining.
  * Move 2: From `(0, 1)` → `(1, 1)` to collect the litter `'L'`.
* The student collects all the litter using 2 moves. Thus, the output is 2.

**Example 2:**
<pre>
<strong>Input:</strong> classroom = ["LS", "RL"], energy = 4
<strong>Output:</strong> 3
</pre>

**Explanation:**

* The student starts at cell `(0, 1)` with 4 units of energy.
* A valid sequence of moves to collect all litter is as follows:
  * Move 1: From `(0, 1) → (0, 0)` to collect the first litter `'L'` with 1 unit of energy used and 3 units remaining.
  * Move 2: From `(0, 0) → (1, 0)` to `'R'` to reset and restore energy back to 4.
  * Move 3: From `(1, 0) → (1, 1)` to collect the second litter `'L'`.
* The student collects all the litter using 3 moves. Thus, the output is 3.

**Example 3:**
<pre>
<strong>Input:</strong> classroom = ["L.S", "RXL"], energy = 3
<strong>Output:</strong> -1
</pre>

**Explanation:**

No valid path collects all `'L'`.

<br />

**Constraints:**

* `1 <= m == classroom.length <= 20`
* `1 <= n == classroom[i].length <= 20`
* `classroom[i][j]` is one of `'S'`, `'L'`, `'R'`, `'X'`, or `'.'`
* `1 <= energy <= 50`
* There is exactly **one** `'S'` in the grid.
* There are **at most** 10 `'L'` cells in the grid.

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