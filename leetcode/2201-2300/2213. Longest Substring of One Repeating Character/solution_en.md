# [2213. Longest Substring of One Repeating Character](https://leetcode.com/problems/longest-substring-of-one-repeating-character/)

<code>Hard</code> level 

You are given a **0-indexed** string <code>s</code>. You are also given a **0-indexed** string <code>queryCharacters</code> of length <code>k</code> and a **0-indexed** array of integer **indices** <code>queryIndices</code> of length <code>k</code>, both of which are used to describe <code>k</code> queries.

The <code>i<sup>th</sup></code> query updates the character in <code>s</code> at index <code>queryIndices[i]</code> to the character <code>queryCharacters[i]</code>.

Return *an array* <code>lengths</code> *of length* <code>k</code> *where* <code>lengths[i]</code> *is the ***length*** of the ***longest substring*** of* <code>s</code> *consisting of ***only one repeating*** character ***after*** the* <code>i<sup>th</sup></code> *query is performed*.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "babacc", queryCharacters = "bcb", queryIndices = [1,3,3]
<strong>Output:</strong> [3,3,4]
</pre>

**Explanation:**
- 1<sup>st</sup> query updates s = "b**b**bacc". The longest substring consisting of one repeating character is "bbb" with length 3.
- 2<sup>nd</sup> query updates s = "bbb**c**cc". 
  The longest substring consisting of one repeating character can be "bbb" or "ccc" with length 3.
- 3<sup>rd</sup> query updates s = "bbb**b**cc". The longest substring consisting of one repeating character is "bbbb" with length 4.
Thus, we return [3,3,4].

**Example 2:**
<pre>
<strong>Input:</strong> s = "abyzz", queryCharacters = "aa", queryIndices = [2,1]
<strong>Output:</strong> [2,3]
</pre>

**Explanation:**
- 1<sup>st</sup> query updates s = "ab**a**zz". The longest substring consisting of one repeating character is "zz" with length 2.
- 2<sup>nd</sup> query updates s = "a**a**azz". The longest substring consisting of one repeating character is "aaa" with length 3.
Thus, we return [2,3].  

<br />

**Constraints:**

* <code>1 <= s.length <= 10<sup>5</sup></code>
* <code>s</code> consists of lowercase English letters.
* <code>k == queryCharacters.length == queryIndices.length</code>
* <code>1 <= k <= 10<sup>5</sup></code>
* <code>queryCharacters</code> consists of lowercase English letters.
* <code>0 <= queryIndices[i] < s.length</code>

<br />

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