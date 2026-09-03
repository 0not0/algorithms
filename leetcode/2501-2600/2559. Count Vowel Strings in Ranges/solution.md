# [2559. Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges)  

`Medium` level 

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