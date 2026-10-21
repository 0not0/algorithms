# [3863. Minimum Operations to Sort a String](https://leetcode.com/problems/minimum-operations-to-sort-a-string/)  

`Medium` level 

You are given a string `s` consisting of lowercase English letters.

In one operation, you can select any **substring**<sup>1</sup> of `s` that is **not** the entire string and **sort** it in **non-descending alphabetical** order.

Return the **minimum** number of operations required to make `s` sorted in **non-descending** order. If it is not possible, return -1.

**1.** A **substring** is a contiguous **non-empty** sequence of characters within a string.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> s = "dog"
<strong>Output:</strong> 1
</pre>
**Explanation:​​​​​​​**
* Sort substring `"og"` to `"go"`.
* Now, `s = "dgo"`, which is sorted in ascending order. Thus, the answer is 1.

**Example 2:**
<pre>
<strong>Input:</strong> s = "card"
<strong>Output:</strong> 2
</pre>

**Explanation:**
* Sort substring `"car"` to `"acr"`, so `s = "acrd"`.
* Sort substring `"rd"` to `"dr"`, making `s = "acdr"`, which is sorted in ascending order. Thus, the answer is 2.

**Example 3:**
<pre>
<strong>Input:</strong> s = "gf"
<strong>Output:</strong> -1
</pre>

**Explanation:**
* It is impossible to sort `s` under the given constraints. Thus, the answer is -1.

<br />

**Constraints:**

* <code>1 <= s.length <= 10<sup>5</sup></code>
* `s` consists of only lowercase English letters.

<br />

***

### Solution

**Time complexity:** `O(n)` - scan the string to check whether it is sorted, find minimum and maximum characters, and count their occurrences.  
**Space complexity:** `O(1)` - only a constant number of variables are used.

<br />

**C++**

```cpp
class Solution {
public:
  int minOperations(string s) {
    int n = s.size();

    if(is_sorted(s.begin(), s.end())) return 0;

    if(n == 2) return -1;

    char mn = *min_element(s.begin(), s.end());
    char mx = *max_element(s.begin(), s.end());

    if(s[0] == mn || s[n - 1] == mx) return 1;

    int minCount = count(s.begin(), s.end(), mn);
    int maxCount = count(s.begin(), s.end(), mx);

    if(s[0] == mx && s[n - 1] == mn &&
      minCount == 1 && maxCount == 1) {
      return 3;
    }

    return 2;
  }
};
```

**Java**

```java
class Solution {
  public int minOperations(String s) {
    int n = s.length();

    boolean sorted = true;
    char mn = 'z';
    char mx = 'a';

    for(int i = 0; i < n; i++) {
      char c = s.charAt(i);

      if(i > 0 && s.charAt(i - 1) > c) {
        sorted = false;
      }

      mn = (char) Math.min(mn, c);
      mx = (char) Math.max(mx, c);
    }

    if(sorted) {
      return 0;
    }

    if(n == 2) {
      return -1;
    }

    if(s.charAt(0) == mn || s.charAt(n - 1) == mx) {
      return 1;
    }

    int minCount = 0;
    int maxCount = 0;

    for(int i = 0; i < n; i++) {
        if(s.charAt(i) == mn) minCount++;
        if(s.charAt(i) == mx) maxCount++;
    }

    if(s.charAt(0) == mx && s.charAt(n - 1) == mn &&
      minCount == 1 && maxCount == 1) {
      return 3;
    }

    return 2;
  }
}
```

**Python**

```python
class Solution:
  def minOperations(self, s: str) -> int:
    n = len(s)

    if all(s[i] <= s[i + 1] for i in range(n - 1)):
      return 0

    if n == 2:
      return -1

    mn = min(s)
    mx = max(s)

    if s[0] == mn or s[-1] == mx:
      return 1

    if (s[0] == mx and s[-1] == mn
        and s.count(mn) == 1
        and s.count(mx) == 1):
      return 3

    return 2    
```