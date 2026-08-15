# [3975. Filter Occupied Intervals](https://leetcode.com/problems/filter-occupied-intervals/description/)  

<code>Medium</code> level 

You are given a 2D integer array <code>occupiedIntervals</code>, where <code>occupiedIntervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represents a time interval during which you are occupied. Each interval starts at <code>start<sub>i</sub></code> and ends at <code>end<sub>i</sub></code>, <strong>inclusive</strong>. These intervals may <strong>overlap</strong>.  

You are also given two integers <code>freeStart</code> and <code>freeEnd</code>, which define a free time interval from <code>freeStart</code> to <code>freeEnd</code>, inclusive.  

Your task is to merge <strong>all</strong> occupied intervals that overlap or touch, then remove <strong>all</strong> integer points in the free interval from the merged occupied intervals.  

Two intervals touch if the second interval starts <strong>immediately after</strong> the first one ends. For example, <code>[1, 1]</code> and <code>[2, 2]</code> touch and should be merged into <code>[1, 2]</code>.  

Return the <strong>remaining</strong> occupied intervals in <strong>sorted</strong> order. The returned intervals must be <strong>non-overlapping</strong> and must contain the <strong>minimum</strong> number of intervals possible. If there are no remaining occupied points, return an empty list.  

<strong>Example 1:</strong>

<pre>
<strong>Input:</strong> occupiedIntervals = [[2,6],[4,8],[10,10],[10,12],[14,16]], freeStart = 7, freeEnd = 11  
<strong>Output:</strong> [[2,6],[12,12],[14,16]]
</pre>  

<strong>Explanation:</strong>

<li>After merging, the occupied intervals are <code>[2, 8]</code>, <code>[10, 12]</code>, and <code>[14, 16]</code>.</li>
<li>Excluding the free interval <code>[7, 11]</code> results in <code>[2, 6]</code>, <code>[12, 12]</code>, and <code>[14, 16]</code>.</li>  
<br /> 

<strong>Example 2:</strong>

<pre>
<strong>Input:</strong> occupiedIntervals = [[1,5],[2,3]], freeStart = 3, freeEnd = 8
<strong>Output:</strong> [[1,2]]
</pre>

<strong>Explanation:</strong>

<li>After merging, the occupied interval is <code>[1, 5]</code>.</li>
<li>Excluding the free interval <code>[3, 8]</code> results in <code>[1, 2]</code>.</li>  
<br />
<strong>Constraints:</strong>  

<li><code>1 <= occupiedIntervals.length <= 5 * 10<sup>4</sup></code></li>
<li><code>occupiedIntervals[i].length == 2</code></li>
<li><code>1 <= start<sub>i</sub> <= end<sub>i</sub> <= 10<sup>9</sup></code></li>
<li><code>1 <= freeStart <= freeEnd <= 10<sup>9</sup></code></li>  

***


<h3>Solution</h3>  

<strong>Time complexity:</strong> <code>O(n log n)</code> - due to sorting the intervals  
<strong>Space complexity:</strong> <code>O(n)</code>

<strong>C++</strong>

```C++
class Solution {
public:
    vector<vector<int>> filterOccupiedIntervals(vector<vector<int>>& occupiedIntervals, int freeStart, int freeEnd) {
        sort(occupiedIntervals.begin(), occupiedIntervals.end());

        vector<vector<int>> merged;

        for (auto& interval : occupiedIntervals) {
            int start = interval[0];
            int end = interval[1];

            if (merged.empty() || merged.back()[1] + 1 < start) {
                merged.push_back({start, end});
            } else {
                merged.back()[1] = max(merged.back()[1], end);
            }
        }

        vector<vector<int>> ans;

        for (auto& interval : merged) {
            int start = interval[0];
            int end = interval[1];

            if (start < freeStart) {
                ans.push_back({start, min(end, freeStart - 1)});
            }

            if (end > freeEnd) {
                ans.push_back({max(start, freeEnd + 1), end});
            }
        }

        return ans;
    }
};
```