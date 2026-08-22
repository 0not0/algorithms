# [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/description/)  

<code>Medium</code> level  

You are a hiker preparing for an upcoming hike. You are given <code>heights</code>, a 2D array of size <code>rows x columns</code>, where <code>heights[row][col]</code> represents the height of cell <code>(row, col)</code>. You are situated in the top-left cell, <code>(0, 0)</code>, and you hope to travel to the bottom-right cell, <code>(rows-1, columns-1)</code> (i.e., **0-indexed**). You can move **up, down, left**, or **right**, and you wish to find a route that requires the minimum **effort**.

A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the *minimum **effort** required to travel from the top-left cell to the bottom-right cell*.  

**Example 1:**

![image for example 1](../../images/dikstra/1631/first.png)

<pre>
<strong>Input:</strong> heights = [[1,2,2],[3,8,2],[5,3,5]]
<strong>Output:</strong> 2
</pre>

**Explanation:**  
The route of [1,3,5,3,5] has a maximum absolute difference of 2 in consecutive cells.
This is better than the route of [1,2,2,2,5], where the maximum absolute difference is 3.  

**Example 2:**  

![image for example 2](../../images/dikstra/1631/second.png)

<pre>
<strong>Input:</strong> heights = [[1,2,3],[3,8,4],[5,3,5]]
<strong>Output:</strong> 1
</pre>

**Explanation:**  
The route of [1,2,3,4,5] has a maximum absolute difference of 1 in consecutive cells, which is better than route [1,3,5,3,5].

**Example 3:**

![image for example 3](../../images/dikstra/1631/third.png)

<pre>
<strong>Input:</strong> heights = [[1,2,1,1,1],[1,2,1,2,1],[1,2,1,2,1],[1,2,1,2,1],[1,1,1,2,1]]
<strong>Output:</strong> 0
</pre>

**Explanation:**  
This route does not require any effort.  

**Constraints:**

* <code>rows == heights.length</code>
* <code>columns == heights[i].length</code>
* <code>1 <= rows, columns <= 100</code>
* <code>1 <= heights[i][j] <= 10<sup>6</sup></code>

***

### Solution  

Головна складність цієї задачи - зрозуміти, як рахувати відстань.  
У звичайному алгоритмі Дейкстри задача -  знайти шлях із мінімальною сумою ваг. <code>newDistance = currentDistance + edgeWeight;</code>.  
Тут Дейкстра для пошуку шляху з мінімальним максимальним ребром - потрібен найбільший перепад між найбільшим перепадом, який уже був на шляху, та перепадом на новому кроці: <code>newEffort = max(currentEffort, edgeWeight);</code>, де:  
<code>edgeWeight = abs(heights[currentRow][currentCol] - heights[nextRow][nextCol]);</code>  
а <code>currentEffort</code> - не є вагою одного ребра, а вже накопичений максимум усіх ребер пройденого шляху.  
Все інше: priority_queue, релаксація, матриця найкращих значень, пропуск застарілих записів - як в класичному Дейкстра.  
 
<strong>Time complexity:</strong> <code>O(rows × columns × log(rows × columns))</code>  
<strong>Space complexity:</strong> <code>O(rows × columns)</code>   

**C++**
```C++
class Solution {
public:
  int minimumEffortPath(vector<vector<int>>& heights) {
    int rows = heights.size();
    int columns = heights[0].size();

    vector<vector<int>> effort(rows, vector<int>(columns, INT_MAX));

    priority_queue<tuple<int, int, int>, vector<tuple<int, int, int>>, greater<tuple<int, int, int>>> minHeap;

    effort[0][0] = 0;
    minHeap.push({0, 0, 0});

    int directions[4][2] = { {1, 0}, {-1, 0}, {0, 1}, {0, -1} };

    while (!minHeap.empty()) {
      auto [currentEffort, row, column] = minHeap.top();
      minHeap.pop();

      if (row == rows - 1 && column == columns - 1) {
          return currentEffort;
      }

      if (currentEffort > effort[row][column]) continue;

      for (auto& direction : directions) {
        int nextRow = row + direction[0];
        int nextColumn = column + direction[1];

        if (nextRow < 0 || nextRow >= rows || nextColumn < 0 || nextColumn >= columns) continue;

        int heightDifference = abs(heights[row][column] - heights[nextRow][nextColumn]);

        int newEffort = max(currentEffort, heightDifference);

        if (newEffort < effort[nextRow][nextColumn]) {
          effort[nextRow][nextColumn] = newEffort;

          minHeap.push({ newEffort, nextRow, nextColumn });
        }
      }
    }

    return 0;
  }
};
```
