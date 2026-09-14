# [3414. Maximum Score of Non-overlapping Intervals](https://leetcode.com/problems/maximum-score-of-non-overlapping-intervals/)  

`Hard` level  

You are given a 2D integer array `intervals`, where <code>intervals[i] = [l<sub>i</sub>, r<sub>i</sub>, weight<sub>i</sub>]</code>. Interval `i` starts at position <code>l<sub>i</sub></code> and ends at <code>r<sub>i</sub></code>, and has a weight of <code>weight<sub>i</sub></code>. You can choose *up to* 4 **non-overlapping** intervals. The **score** of the chosen intervals is defined as the total sum of their weights.

Return the **lexicographically smallest**<sup>1</sup> array of at most 4 indices from `intervals` with **maximum** score, representing your choice of non-overlapping intervals.

Two intervals are said to be **non-overlapping** if they do not share any points. In particular, intervals sharing a left or right boundary are considered overlapping.  

**1.** An array `a` is **lexicographically smaller** than an array `b` if in the first position where `a` and `b` differ, array `a` has an element that is less than the corresponding element in `b`.
If the first `min(a.length, b.length)` elements do not differ, then the shorter array is the lexicographically smaller one.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> intervals = [[1,3,2],[4,5,2],[1,5,5],[6,9,3],[6,7,1],[8,9,1]]
<strong>Output:</strong> [2,3]
<strong>Explanation:</strong>
You can choose the intervals with indices 2, and 3 with respective weights of 5, and 3.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> intervals = [[5,8,1],[6,7,7],[4,7,3],[9,10,6],[7,8,2],[11,14,3],[3,5,5]]
<strong>Output:</strong> [1,3,5,6]
<strong>Explanation:</strong>
You can choose the intervals with indices 1, 3, 5, and 6 with respective weights of 7, 6, 3, and 5.  
</pre> 

<br />  

**Constraints:**

* <code>1 <= intevals.length <= 5 * 10<sup>4</sup></code>
* <code>intervals[i].length == 3</code>
* <code>intervals[i] = [l<sub>i</sub>, r<sub>i</sub>, weight<sub>i</sub>]</code>
* <code>1 <= l<sub>i</sub> <= r<sub>i</sub> <= 10<sup>9</sup></code>
* <code>1 <= weight<sub>i</sub> <= 10<sup>9</sup></code>  

<br />

***

### Solution

**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n)`

**C++**

```cpp
class Solution {
public:
  struct State 
  {
    long long score = 0;
    array<int, 4> idx = {};
    int size = 0;
  };

  bool isBetter(const State& a, const State& b)
  {
    if(a.score != b.score) return a.score > b.score;

    for(int i = 0; i < min(a.size, b.size); i++)
      if(a.idx[i] != b.idx[i]) return a.idx[i] < b.idx[i];

    return a.size < b.size;
  }

  State addIndex(State state, int index)
  {
    int pos = state.size;

    while(pos > 0 && state.idx[pos - 1] > index)
    {
      state.idx[pos] = state.idx[pos - 1];
      pos--;
    }

    state.idx[pos] = index;
    state.size++;

    return state;
  }

  vector<int> maximumWeight(vector<vector<int>>& intervals) {
    int n = intervals.size();
    vector<array<long long, 4>> arr(n);

    for(int i = 0; i < n; i++)
    {
      arr[i] = 
      {
        intervals[i][0],
        intervals[i][1],
        intervals[i][2],
        i
      };
    }

    sort(arr.begin(), arr.end(), [](const auto& a, const auto& b) { return a[1] < b[1]; });

    vector<long long> ends(n);

    for(int i = 0; i < n; i++) ends[i] = arr[i][1];

    vector<int> prev(n);

    for(int i = 0; i < n; i++)
      prev[i] = lower_bound(ends.begin(), ends.begin() + i, arr[i][0]) - ends.begin() - 1;

    vector<array<State, 5>> dp(n + 1);

    for(int i = 1; i <= n; i++)
    {
      for(int j = 1; j <= 4; j++)
      {
        State skip = dp[i - 1][j];

        State take = dp[prev[i - 1] + 1][j - 1];
        take.score += arr[i - 1][2];
        take = addIndex(take, arr[i - 1][3]);

        dp[i][j] = isBetter(take, skip) ? take : skip;
      }
    }

    State& ans = dp[n][4];

    return vector<int>(ans.idx.begin(), ans.idx.begin() + ans.size);
  }
};
```

<br />
 
**Java**

```java
import java.util.*;

class Solution {
  static class State {
    long score;
    int[] idx = new int[4];
    int size;
  }

  private boolean isBetter(State a, State b) {
    if(a.score != b.score) return a.score > b.score;

    for(int i = 0; i < Math.min(a.size, b.size); i++) {
      if(a.idx[i] != b.idx[i]) return a.idx[i] < b.idx[i];
    }

    return a.size < b.size;
  }

  private State copyState(State state) {
    State copy = new State();
    copy.score = state.score;
    copy.size = state.size;
    copy.idx = state.idx.clone();

    return copy;
  }

  private State addIndex(State state, int index) {
    State res = copyState(state);

    int pos = res.size;

    while (pos > 0 && res.idx[pos - 1] > index) {
      res.idx[pos] = res.idx[pos - 1];
      pos--;
    }

    res.idx[pos] = index;
    res.size++;

    return res;
  }

  public int[] maximumWeight(List<List<Integer>> intervals) {
    int n = intervals.size();

    long[][] arr = new long[n][4];

    for(int i = 0; i < n; i++) {
      arr[i][0] = intervals.get(i).get(0);
      arr[i][1] = intervals.get(i).get(1);
      arr[i][2] = intervals.get(i).get(2);
      arr[i][3] = i;
    }

    Arrays.sort(arr, Comparator.comparingLong(a -> a[1]));

    long[] ends = new long[n];

    for(int i = 0; i < n; i++) ends[i] = arr[i][1];

    int[] prev = new int[n];

    for(int i = 0; i < n; i++) {
      int left = 0;
      int right = i;

      while(left < right) {
        int mid = left + (right - left) / 2;

        if (ends[mid] < arr[i][0]) {
          left = mid + 1;
        } else {
          right = mid;
        }
      }

      prev[i] = left - 1;
    }

    State[][] dp = new State[n + 1][5];

    for(int i = 0; i <= n; i++) {
      for(int j = 0; j <= 4; j++) {
        dp[i][j] = new State();
      }
    }

    for(int i = 1; i <= n; i++) {
      for(int j = 1; j <= 4; j++) {
        State skip = dp[i - 1][j];

        State take = addIndex(dp[prev[i - 1] + 1][j - 1], (int) arr[i - 1][3]);

        take.score += arr[i - 1][2];

        dp[i][j] = isBetter(take, skip) ? take : copyState(skip);
      }
    }

    State ans = dp[n][4];

    return Arrays.copyOf(ans.idx, ans.size);
  }
}
```

<br />

**JavaScript**

```javascript
var maximumWeight = function(intervals) {
  const n = intervals.length;

  const arr = intervals.map((interval, i) => [
    interval[0],
    interval[1],
    interval[2],
    i
  ]);

  arr.sort((a, b) => a[1] - b[1]);

  const ends = arr.map(x => x[1]);
  const prev = new Array(n);

  for(let i = 0; i < n; i++) {
    let left = 0;
    let right = i;

    while(left < right) {
      const mid = Math.floor((left + right) / 2);

      if(ends[mid] < arr[i][0]) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }

    prev[i] = left - 1;
  }

  const isBetter = (a, b) => {
    if(a.score !== b.score) return a.score > b.score;

    const len = Math.min(a.idx.length, b.idx.length);

    for(let i = 0; i < len; i++) {
      if (a.idx[i] !== b.idx[i]) return a.idx[i] < b.idx[i];
    }

    return a.idx.length < b.idx.length;
  };

  const addIndex = (state, index) => {
    const idx = [...state.idx];
    let pos = idx.length;
    idx.push(index);

    while(pos > 0 && idx[pos - 1] > index) {
      idx[pos] = idx[pos - 1];
      pos--;
    }

    idx[pos] = index;

    return {
      score: state.score,
      idx
    };
  };

  const dp = Array.from({ length: n + 1 }, () =>
    Array.from({ length: 5 }, () => ({
      score: 0,
      idx: []
    }))
  );

  for(let i = 1; i <= n; i++) {
    for(let j = 1; j <= 4; j++) {
      const skip = dp[i - 1][j];

      const take = addIndex(dp[prev[i - 1] + 1][j - 1], arr[i - 1][3]);

      take.score += arr[i - 1][2];

      dp[i][j] = isBetter(take, skip) ? take : skip;
    }
  }

  return dp[n][4].idx;
};
```

<br />

**TypeScript** 

```typescript
type State = {
  score: number;
  idx: number[];
};

function maximumWeight(intervals: number[][]): number[] {
  const n = intervals.length;

  const arr: number[][] = intervals.map((interval, i) => [
    interval[0],
    interval[1],
    interval[2],
    i
  ]);

  arr.sort((a, b) => a[1] - b[1]);

  const ends: number[] = arr.map(x => x[1]);
  const prev: number[] = new Array(n);

  for(let i = 0; i < n; i++) {
    let left = 0;
    let right = i;

    while(left < right) {
      const mid = Math.floor((left + right) / 2);

      if(ends[mid] < arr[i][0]) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }

    prev[i] = left - 1;
  }

  const isBetter = (a: State, b: State): boolean => {
    if(a.score !== b.score) return a.score > b.score;

    const len = Math.min(a.idx.length, b.idx.length);

    for(let i = 0; i < len; i++)
      if(a.idx[i] !== b.idx[i]) return a.idx[i] < b.idx[i];

    return a.idx.length < b.idx.length;
  };

  const addIndex = (state: State, index: number): State => {
    const idx = [...state.idx];
    let pos = idx.length;

    idx.push(index);

    while(pos > 0 && idx[pos - 1] > index) {
      idx[pos] = idx[pos - 1];
      pos--;
    }

    idx[pos] = index;

    return {
      score: state.score,
      idx
    };
  };

  const dp: State[][] = Array.from({ length: n + 1 }, () => 
    Array.from({ length: 5 }, () => ({score: 0, idx: []})));

  for(let i = 1; i <= n; i++) {
    for(let j = 1; j <= 4; j++) {
      const skip = dp[i - 1][j];
      const take = addIndex(dp[prev[i - 1] + 1][j - 1], arr[i - 1][3]);

      take.score += arr[i - 1][2];

      dp[i][j] = isBetter(take, skip) ? take : skip;
    }
  }

  return dp[n][4].idx;
}
```

<br />

**Python** 

```python
class Solution:
  def maximumWeight(self, intervals: List[List[int]]) -> List[int]:
    n = len(intervals)

    arr = [
      [l, r, w, i]
      for i, (l, r, w) in enumerate(intervals)
    ]

    arr.sort(key=lambda x: x[1])

    ends = [x[1] for x in arr]
    prev = [0] * n

    for i in range(n):
      left = 0
      right = i

      while left < right:
        mid = (left + right) // 2

        if ends[mid] < arr[i][0]:
          left = mid + 1
        else:
          right = mid

      prev[i] = left - 1

      def is_better(a, b):
        if a[0] != b[0]:
          return a[0] > b[0]

        return a[1] < b[1]

      def add_index(state, index):
        score, indices = state

        indices = indices[:]

        pos = len(indices)
        indices.append(index)

        while pos > 0 and indices[pos - 1] > index:
          indices[pos] = indices[pos - 1]
          pos -= 1

        indices[pos] = index

        return score, indices

      dp = [
        [(0, []) for _ in range(5)]
        for _ in range(n + 1)
      ]

      for i in range(1, n + 1):
        for j in range(1, 5):
          skip = dp[i - 1][j]

          score, indices = add_index(dp[prev[i - 1] + 1][j - 1], arr[i - 1][3])

          take = (score + arr[i - 1][2], indices)

          dp[i][j] = take if is_better(take, skip) else skip

    return dp[n][4][1]
```