# [3501. Maximize Active Section with Trade II](https://leetcode.com/problems/maximize-active-section-with-trade-ii/)  

<code>Hard</code> level 

You are given a binary string <code>s</code> of length <code>n</code>, where:

* <code>'1'</code> represents an **active** section.
* <code>'0'</code> represents an **inactive** section.  
  
You can perform **at most one trade** to maximize the number of active sections in <code>s</code>. In a trade, you:

* Convert a contiguous block of <code>'1'</code>s that is surrounded by <code>'0'</code>s to all <code>'0'</code>s.
* Afterward, convert a contiguous block of <code>'0'</code>s that is surrounded by <code>'1'</code>s to all <code>'1'</code>s.  

Additionally, you are given a **2D array** <code>queries</code>, where <code>queries[i] = [li, ri]</code> represents a substring <code>s[li...ri]</code>.

For each query, determine the **maximum** possible number of active sections in <code>s</code> after making the optimal trade on the substring <code>s[li...ri]</code>.

Return an array <code>answer</code>, where <code>answer[i]</code> is the result for <code>queries[i]</code>.

**Note**

* For each query, treat <code>s[li...ri]</code> as if it is **augmented** with a <code>'1'</code> at both ends, forming <code>t = '1' + s[li...ri] + '1'</code>. The augmented <code>'1'</code>s **do not** contribute to the final count.
* The queries are independent of each other.  
  
<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "01", queries = [[0,1]]
<strong>Output:</strong> [1]
</pre>  

**Explanation:**

Because there is no block of <code>'1'</code>s surrounded by <code>'0'</code>s, no valid trade is possible. The maximum number of active sections is 1.  

**Example 2:**
<pre>
<strong>Input:</strong> s = "0100", queries = [[0,3],[0,2],[1,3],[2,3]]
<strong>Output:</strong> [4,3,1,1]
</pre>  

**Explanation:**

* Query <code>[0, 3]</code> → Substring <code>"0100"</code> → Augmented to <code>"101001"</code>
Choose <code>"0100"</code>, convert <code>"0100"</code> → <code>"0000"</code> → <code>"1111"</code>.
The final string without augmentation is <code>"1111"</code>. The maximum number of active sections is 4.

* Query <code>[0, 2]</code> → Substring <code>"010"</code> → Augmented to <code>"10101"</code>
Choose <code>"010"</code>, convert <code>"010"</code> → <code>"000"</code> → <code>"111"</code>.
The final string without augmentation is <code>"1110"</code>. The maximum number of active sections is 3.

* Query <code>[1, 3]</code> → Substring <code>"100"</code> → Augmented to <code>"11001"</code>
Because there is no block of <code>'1'</code>s surrounded by <code>'0'</code>s, no valid trade is possible. The maximum number of active sections is 1.

* Query <code>[2, 3]</code> → Substring <code>"00"</code> → Augmented to <code>"1001"</code>
Because there is no block of <code>'1'</code>s surrounded by <code>'0'</code>s, no valid trade is possible. The maximum number of active sections is 1.  

**Example 3:**
<pre>
<strong>Input:</strong> s = "1000100", queries = [[1,5],[0,6],[0,4]]
<strong>Output:</strong> [6,7,2]
</pre>  

**Explanation:**

* Query <code>[1, 5]</code> → Substring <code>"00010"</code> → Augmented to <code>"1000101"</code>
Choose <code>"00010"</code>, convert <code>"00010"</code> → <code>"00000"</code> → <code>"11111"</code>.
The final string without augmentation is <code>"1111110"</code>. The maximum number of active sections is 6.

* Query <code>[0, 6]</code> → Substring <code>"1000100"</code> → Augmented to <code>"110001001"</code>
Choose <code>"000100"</code>, convert <code>"000100"</code> → <code>"000000"</code> → <code>"111111"</code>.
The final string without augmentation is <code>"1111111"</code>. The maximum number of active sections is 7.

* Query <code>[0, 4]</code> → Substring <code>"10001"</code> → Augmented to <code>"1100011"</code>
Because there is no block of <code>'1'</code>s surrounded by <code>'0'</code>s, no valid trade is possible. The maximum number of active sections is 2.

**Example 4:**
<pre>
<strong>Input:</strong> s = "01010", queries = [[0,3],[1,4],[1,3]]
<strong>Output:</strong> [4,4,2]
</pre>  

**Explanation:**

* Query <code>[0, 3]</code> → Substring <code>"0101"</code> → Augmented to <code>"101011"</code>
Choose <code>"010"</code>, convert <code>"010"</code> → <code>"000"</code> → <code>"111"</code>.
The final string without augmentation is <code>"11110"</code>. The maximum number of active sections is 4.

* Query <code>[1, 4]</code> → Substring <code>"1010"</code> → Augmented to <code>"110101"</code>
Choose <code>"010"</code>, convert <code>"010"</code> → <code>"000"</code> → <code>"111"</code>.
The final string without augmentation is <code>"01111"</code>. The maximum number of active sections is 4.

* Query <code>[1, 3]</code> → Substring <code>"101"</code> → Augmented to <code>"11011"</code>
Because there is no block of <code>'1'</code>s surrounded by <code>'0'</code>s, no valid trade is possible. The maximum number of active sections is 2.  

**Constraints:**

* <code>1 <= n == s.length <= 10<sup>5</sup></code>
* <code>1 <= queries.length <= 10<sup>5</sup></code>
* <code>s[i]</code> is either <code>'0'</code> or <code>'1'.</code>
* <code>queries[i] = [l<sub>i</sub>, r<sub>i</sub>]</code>
* <code>0 <= l<sub>i</sub> <= r<sub>i</sub> < n</code>

<br />

***

### Solution  

**Time complexity:**  <code>O(n + qlogn)</code>  
**Space complexity:**  <code>O(n)</code>  
**where:**
<code>q = queries.length</code>

**C++**

```C++
class Solution {
private:
  struct ZeroGroup {
    int start;
    int length;
  };

  class SegmentTree {
  private:
    int size = 1;
    vector<int> tree;

  public:
    SegmentTree(const vector<int>& values) {
      while (size < static_cast<int>(values.size())) {
        size *= 2;
      }

      tree.assign(size * 2, 0);

      for (int i = 0; i < static_cast<int>(values.size()); ++i) {
        tree[size + i] = values[i];
      }

      for (int i = size - 1; i >= 1; --i) {
        tree[i] = max(tree[i * 2], tree[i * 2 + 1]);
      }
    }

    int query(int left, int right) const {
      if (left > right) return 0;

      left += size;
      right += size;
      int result = 0;

      while (left <= right) {
        if (left % 2 == 1) {
          result = max(result, tree[left]);
          ++left;
        }

        if (right % 2 == 0) {
          result = max(result, tree[right]);
          --right;
        }

        left /= 2;
        right /= 2;
      }

      return result;
    }
  };

public:
  vector<int> maxActiveSectionsAfterTrade(string s, vector<vector<int>>& queries) {
    const int n = static_cast<int>(s.size());
    int totalOnes = 0;

    for (char c : s) {
      if (c == '1') {
        ++totalOnes;
      }
    }

    vector<ZeroGroup> zeroGroups;
    vector<int> groupAt(n, -1);

    for (int i = 0; i < n; ++i) {
      if (s[i] == '0') {
        if (i > 0 && s[i - 1] == '0') {
          ++zeroGroups.back().length;
        } else {
          zeroGroups.push_back({i, 1});
        }
      }

      groupAt[i] = static_cast<int>(zeroGroups.size()) - 1;
    }

    auto relominexa = make_pair(s, queries);

    if (zeroGroups.empty()) return vector<int>(queries.size(), totalOnes);

    vector<int> pairGain;

    for (int i = 0; i + 1 < static_cast<int>(zeroGroups.size()); ++i) {
      pairGain.push_back(zeroGroups[i].length + zeroGroups[i + 1].length);
    }

    SegmentTree segmentTree(pairGain);

    vector<int> answer;
    answer.reserve(queries.size());

    for (const vector<int>& query : queries) {
      int l = query[0];
      int r = query[1];
      int result = totalOnes;
      int leftPart = -1;

      if (s[l] == '0') {
        int groupId = groupAt[l];
        const ZeroGroup& group = zeroGroups[groupId];

        leftPart = group.length - (l - group.start);
      }

      int rightPart = -1;

      if (s[r] == '0') {
        int groupId = groupAt[r];
        const ZeroGroup& group = zeroGroups[groupId];

        rightPart = r - group.start + 1;
      }


      int firstFullGroup = groupAt[l] + 1;
      int lastFullGroup = s[r] == '1' ? groupAt[r] : groupAt[r] - 1;

      if (firstFullGroup <= lastFullGroup - 1) {
        int gain = segmentTree.query(firstFullGroup, lastFullGroup - 1);

        result = max(result, totalOnes + gain);
      }

      if (s[l] == '0' && s[r] == '0' && groupAt[l] + 1 == groupAt[r]) {
        result = max(result, totalOnes + leftPart + rightPart);
      }

      if (s[l] == '0' && groupAt[l] + 1 <= lastFullGroup) {
        int nextGroup = groupAt[l] + 1;

        result = max(result, totalOnes + leftPart + zeroGroups[nextGroup].length);
      }

      if (s[r] == '0' && groupAt[l] < groupAt[r] - 1) {
        int previousGroup = groupAt[r] - 1;

        result = max(result, totalOnes + zeroGroups[previousGroup].length + rightPart);
      }

      answer.push_back(result);
    }

    return answer;
  }
};
```