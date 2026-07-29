# [3501. Maximize Active Section with Trade II](https://leetcode.com/problems/maximize-active-section-with-trade-ii/)  

<code>Hard</code> level 


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