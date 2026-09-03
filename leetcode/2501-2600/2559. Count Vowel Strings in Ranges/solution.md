# [2559. Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges)  

`Medium` level 

You are given a **0-indexed** array of strings `words` and a 2D array of integers `queries`.

Each query <code>queries[i] = [l<sup>i</sup>, r<sup>i</sup>]</code> asks us to find the number of strings present at the indices ranging from <code>l<sup>i</sup></code> to <code>r<sup>i</sup></code> (both **inclusive**) of `words` that start and end with a vowel.

Return *an array* `ans` *of size* `queries.length`, *where* `ans[i]` *is the answer to the* <code>i<sup>th</sup></code> *query*.

**Note** that the vowel letters are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> words = ["aba","bcb","ece","aa","e"], queries = [[0,2],[1,4],[1,1]]
<strong>Output:</strong> [2,3,0]
<strong>Explanation:</strong> The strings starting and ending with a vowel are "aba", "ece", "aa" and "e".
The answer to the query [0,2] is 2 (strings "aba" and "ece").
to query [1,4] is 3 (strings "ece", "aa", "e").
to query [1,1] is 0.
We return [2,3,0].
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> words = ["a","e","i"], queries = [[0,2],[0,1],[2,2]]
<strong>Output:</strong> [3,2,1]
<strong>Explanation:</strong> Every string satisfies the conditions, so we return [3,2,1].
</pre>

<br />

**Constraints:**

* <code>1 <= words.length <= 10<sup>5</sup></code>
* <code>1 <= words[i].length <= 40</code>
* <code>words[i]</code> consists only of lowercase English letters.
* <code>sum(words[i].length) <= 3 * 10<sup>5</sup></code>
* <code>1 <= queries.length <= 10<sup>5</sup></code>
* <code>0 <= l<sub>i</sub> <= r<sub>i</sub> < words.length</code>

<br />

***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```C++
class Solution {
public:
  vector<int> vowelStrings(vector<string>& words, vector<vector<int>>& queries) {
    int n = words.size();

    vector<int> prefix(n + 1);

    auto isVowel = [](char c)
    {
      return c == 'a' || c == 'e' || c == 'i' ||
        c == 'o' || c == 'u';
    };

    for(int i = 0; i < n; i++)
    {
      bool valid = isVowel(words[i].front()) && isVowel(words[i].back());

      prefix[i + 1] = prefix[i] + valid;
    }

    vector<int> result;

    for(const auto& query : queries)
    {
      int left = query[0];
      int right = query[1];

      result.push_back(prefix[right + 1] - prefix[left]);
    }

    return result;
  }
};
``