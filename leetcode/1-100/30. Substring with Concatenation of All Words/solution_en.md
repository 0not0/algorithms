# [30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)  

**Hard** level  

You are given a string <code>s</code> and an array of strings <code>words</code>. All the strings of <code>words</code> are of **the same length**.

A **concatenated string** is a string that exactly contains all the strings of any permutation of <code>words</code> concatenated.

* For example, if <code>words = ["ab","cd","ef"]</code>, then <code>"abcdef"</code>, <code>"abefcd"</code>, <code>"cdabef"</code>, <code>"cdefab"</code>, <code>"efabcd"</code>, and <code>"efcdab"</code> are all concatenated strings. <code>"acdbef"</code> is not a concatenated string because it is not the concatenation of any permutation of <code>words</code>.  
  
Return an array of *the starting indices* of all the concatenated substrings in <code>s</code>. You can return the answer in **any order**. 

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "barfoothefoobarman", words = ["foo","bar"]
<strong>Output:</strong> [0,9]
</pre>
**Explanation:**

The substring starting at 0 is <code>"barfoo"</code>. It is the concatenation of <code>["bar","foo"]</code> which is a permutation of <code>words</code>.
The substring starting at 9 is <code>"foobar"</code>. It is the concatenation of <code>["foo","bar"]</code> which is a permutation of <code>words</code>.

**Example 2:**
<pre>
<strong>Input:</strong> s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
<strong>Output:</strong> []
</pre>
**Explanation:**

There is no concatenated substring.

**Example 3:**
<pre>
<strong>Input:</strong> s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
<strong>Output:</strong> [6,9,12]
</pre>
**Explanation:**

The substring starting at 6 is <code>"foobarthe"</code>. It is the concatenation of <code>["foo","bar","the"]</code>.
The substring starting at 9 is <code>"barthefoo"</code>. It is the concatenation of <code>["bar","the","foo"]</code>.
The substring starting at 12 is <code>"thefoobar"</code>. It is the concatenation of <code>["the","foo","bar"]</code>.

<br />

**Constraints:**

* <code>1 <= s.length <= 10<sup>4</sup></code>
* <code>1 <= words.length <= 5000</code>
* <code>1 <= words[i].length <= 30</code>
* <code>s</code> and <code>words[i]</code> consist of lowercase English letters.

<br />

***  

### Solution

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(m)</code>  
<code>m = words.size()</code>

**C++**
```C++
class Solution
{
  public:
    vector<int> findSubstring(string s, vector<string>& words)
    {
      const int n = s.size();
      const int wordsCount = words.size();
      const int wordLength = words[0].size();

      unordered_map<string, int> required;

      for(const string& word : words) required[word]++;

      vector<int> result;

      for(int offset = 0; offset < wordLength; offset++)
      {
        int left = offset;
        int right = offset;
        int currentWords = 0;

        unordered_map<string, int> window;

        while(right + wordLength <= n)
        {
          string word = s.substr(right, wordLength);
          right += wordLength;

          if(!required.contains(word))
          {
            window.clear();
            currentWords = 0;
            left = right;

            continue;
          }

          window[word]++;
          currentWords++;

          while(window[word] > required[word])
          {
            string leftWord = s.substr(left, wordLength);

            window[leftWord]--;
            currentWords--;

            left += wordLength;
          }

          if(currentWords == wordsCount)
          {
            result.push_back(left);
            string leftWord = s.substr(left, wordLength);

            window[leftWord]--;
            currentWords--;

            left += wordLength;
          }
        }
      }

      return result;
    }
};
```

**JavaScript**
```JS
var findSubstring = function(s, words) {
  const n = s.length;
  const wordsCount = words.length;
  const wordLength = words[0].length;

  const required = new Map();

  for(const word of words) {
    required.set(word, (required.get(word) || 0) + 1);
  }

  const result = [];

  for(let offset = 0; offset < wordLength; offset++) {
    let left = offset;
    let right = offset;
    let currentWords = 0;

    const window = new Map();

    while(right + wordLength <= n) {
      const word = s.slice(right, right + wordLength);
      right += wordLength;

      if(!required.has(word)) {
        window.clear();
        currentWords = 0;
        left = right;

        continue;
      }

      window.set(word, (window.get(word) || 0) + 1);
      currentWords++;

      while(window.get(word) > required.get(word)) {
        const leftWord = s.slice(left, left + wordLength);

        window.set(leftWord, window.get(leftWord) - 1);
        currentWords--;

        left += wordLength;
      }

      if(currentWords === wordsCount) {
        result.push(left);

        const leftWord = s.slice(left, left + wordLength);

        window.set(leftWord, window.get(leftWord) - 1);
        currentWords--;

        left += wordLength;
      }
    }
  }

  return result;
};
```