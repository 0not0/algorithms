# [2213. Longest Substring of One Repeating Character](https://leetcode.com/problems/longest-substring-of-one-repeating-character/)

<code>Hard</code> level 

***

### Solution  

**Time complexity:**  <code>O(n + k * log n)</code>  
**Space complexity:**  <code>O(n)</code>   

**C++**  
```C++
class Solution {
  struct Node
  {
    int pref = 1;
    int suff = 1;
    int best = 1;
    char leftChar;
    char rightChar;
  };

  vector<Node> tree;

  Node merge(const Node& a, const Node& b, int leftLen, int rightLen) 
  {
    Node res;

    res.leftChar = a.leftChar;
    res.rightChar = b.rightChar;

    res.pref = a.pref;
    res.suff = b.suff;
    res.best = max(a.best, b.best);

    if(a.rightChar == b.leftChar)
    {
      res.best = max(res.best, a.suff + b.pref);

      if(a.pref == leftLen) res.pref += b.pref;

      if(b.suff == rightLen) res.suff += a.suff;
    }

    return res;
  }

  void build(int node, int l, int r, const string& s)
  {
    if(l == r)
    {
      tree[node].leftChar = tree[node].rightChar = s[l];
      return;
    }

    int mid = (l + r) / 2;

    build(node * 2, l, mid, s);
    build(node * 2 + 1, mid + 1, r, s);

    tree[node] = merge(tree[node * 2], tree[node * 2 + 1], mid - l + 1, r - mid);
  }

  void update(int node, int l, int r, int index, char c)
  {
    if(l == r)
    {
      tree[node].leftChar = tree[node].rightChar = c;
      return;
    }

    int mid = (l + r) / 2;

    if(index <= mid) 
    {
      update(node * 2, l, mid, index, c);
    } else 
    {
      update(node * 2 + 1, mid + 1, r, index, c);
    }

    tree[node] = merge(tree[node * 2], tree[node * 2 + 1], mid - l + 1, r - mid);
  }

public:
  vector<int> longestRepeating(string s, string queryCharacters, vector<int>& queryIndices)
  {
    int n = s.size();
    int k = queryIndices.size();

    tree.resize(4 * n);
    build(1, 0, n - 1, s);

    vector<int> ans;
    ans.reserve(k);

    for(int i = 0; i < k; ++i)
    {
      update(1, 0, n - 1, queryIndices[i], queryCharacters[i]);

      ans.push_back(tree[1].best);
    }

    return ans;
  }
};
```