# [2904. Shortest and Lexicographically Smallest Beautiful String](https://leetcode.com/problems/shortest-and-lexicographically-smallest-beautiful-string)  

<code>Medium</code> level  

You are given a binary string <code>s</code> and a positive integer <code>k</code>.

A substring of <code>s</code> is **beautiful** if the number of <code>1</code>'s in it is exactly <code>k</code>.

Let <code>len</code> be the length of the **shortest** beautiful substring.

Return *the lexicographically **smallest** beautiful substring of string* <code>s</code> *with length equal to* <code>len</code>. If <code>s</code> doesn't contain a beautiful substring, return *an **empty** string*.

A string <code>a</code> is lexicographically **larger** than a string <code>b</code> (of the same length) if in the first position where <code>a</code> and <code>b</code> differ, <code>a</code> has a character strictly larger than the corresponding character in <code>b</code>.

* For example, <code>"abcd"</code> is lexicographically larger than <code>"abcc"</code> because the first position they differ is at the fourth character, and <code>d</code> is greater than <code>c</code>.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "100011001", k = 3
<strong>Output:</strong> "11001"
</pre>
**Explanation:** There are 7 beautiful substrings in this example:
1. The substring "<u>100011</u>001".
2. The substring "<u>1000110</u>01".
3. The substring "<u>10001100</u>1".
4. The substring "1<u>00011001</u>".
5. The substring "10<u>0011001</u>".
6. The substring "100<u>011001</u>".
7. The substring "1000<u>11001</u>".
The length of the shortest beautiful substring is 5.
The lexicographically smallest beautiful substring with length 5 is the substring "11001".

**Example 2:**
<pre>
<strong>Input:</strong> s = "1011", k = 2
<strong>Output:</strong> "11"
</pre>
**Explanation:** There are 3 beautiful substrings in this example:
1. The substring "<u>1011</u>".
2. The substring "1<u>011</u>".
3. The substring "10<u>11</u>".
The length of the shortest beautiful substring is 2.
The lexicographically smallest beautiful substring with length 2 is the substring "11".

**Example 3:**
<pre>
<strong>Input:</strong> s = "000", k = 1
<strong>Output:</strong> ""
</pre>
**Explanation:** There are no beautiful substrings in this example.

<br />

**Constraints:**

* <code>1 <= s.length <= 100</code>
* <code>1 <= k <= s.length</code>

<br />

***  

### Solution

**Time complexity:** <code>O(n<sup>2</sup>)</code>  
**Space complexity:** <code>O(1)</code>  
**<sup>*</sup>** but with output string **Space complexity:** is <code>O(n)</code>

**C++**
```C++
class Solution
{
  public:
    string shortestBeautifulSubstring(string s, int k)
    {
      int n = s.size();
      int left = 0;
      int ones = 0;

      int bLeft = -1;
      int bLen = INT_MAX;

      for(int right = 0; right < n; right++)
      {
        ones += s[right] == '1';

        while(ones > k)
        {
            ones -= s[left] == '1';
            left++;
        }

        while(ones == k && s[left] == '0') left++;

        if(ones != k) continue;

        int len = right - left + 1;

        if(
          len < bLen || 
          (len == bLen &&
          lexicographical_compare(s.begin() + left, s.begin() + right + 1, s.begin() + bLeft, s.begin() + bLeft + bLen))
        )
        {
          bLen = len;
          bLeft = left;
        }
      }

    return bLeft == -1 ? "" : s.substr(bLeft, bLen);
  }
};
```