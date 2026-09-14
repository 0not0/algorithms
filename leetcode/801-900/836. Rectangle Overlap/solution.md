# [836. Rectangle Overlap](https://leetcode.com/problems/rectangle-overlap/)  

`Easy` level  

An axis-aligned rectangle is represented as a list `[x1, y1, x2, y2]`, where `(x1, y1)` is the coordinate of its bottom-left corner, and `(x2, y2)` is the coordinate of its top-right corner. Its top and bottom edges are parallel to the X-axis, and its left and right edges are parallel to the Y-axis.

Two rectangles overlap if the area of their intersection is **positive**. To be clear, two rectangles that only touch at the corner or edges do not overlap.

Given two axis-aligned rectangles `rec1` and `rec2`, return `true` *if they overlap, otherwise return* `false`.

<br />

**Example 1:**

<pre>
<strong>Input:</strong> rec1 = [0, 0, 2, 2], rec2 = [1, 1, 3, 3]  
<strong>Output:</strong> true    
</pre>

**Example 2:**

<pre>
<strong>Input:</strong> rec1 = [0, 0, 1, 1], rec2 = [1, 0, 2, 1]  
<strong>Output:</strong> false    
</pre>

**Example 3:**

<pre>
<strong>Input:</strong> rec1 = [0, 0, 1, 1], rec2 = [2, 2, 3, 3]  
<strong>Output:</strong> false  
</pre>

<br />

**Constraints:**

* `rec1.length == 4`
* `rec2.length == 4`
* <code>-10<sup>9</sup> <= rec1[i], rec2[i] <= 10<sup>9</sup></code>
* `rec1` and `rec2` represent a valid rectangle with a non-zero area.  

<br />

***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```cpp
class Solution {
public:
  bool isRectangleOverlap(vector<int>& rec1, vector<int>& rec2) {
    return max(rec1[0], rec2[0]) < min(rec1[2], rec2[2]) &&
      max(rec1[1], rec2[1]) < min(rec1[3], rec2[3]);
  }
};
```

**Java**

```java
class Solution {
  public boolean isRectangleOverlap(int[] rec1, int[] rec2) {
    return Math.max(rec1[0], rec2[0]) < Math.min(rec1[2], rec2[2]) &&
      Math.max(rec1[1], rec2[1]) < Math.min(rec1[3], rec2[3]);
  }
}
```

**JavaScript**

```JavaScript
var isRectangleOverlap = function(rec1, rec2) {
  return Math.max(rec1[0], rec2[0]) < Math.min(rec1[2], rec2[2]) &&
    Math.max(rec1[1], rec2[1]) < Math.min(rec1[3], rec2[3]);
};
```

**TypeScript**

```typescript
function isRectangleOverlap(rec1: number[], rec2: number[]): boolean {
  return Math.max(rec1[0], rec2[0]) < Math.min(rec1[2], rec2[2]) &&
    Math.max(rec1[1], rec2[1]) < Math.min(rec1[3], rec2[3]);
};
```

**Python**

```python
class Solution:
  def isRectangleOverlap(self, rec1: List[int], rec2: List[int]) -> bool:
    return max(rec1[0], rec2[0]) < min(rec1[2], rec2[2]) and \
      max(rec1[1], rec2[1]) < min(rec1[3], rec2[3])
```