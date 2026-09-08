# [3870. Count Commas in Range](https://leetcode.com/problems/count-commas-in-range/)

`Easy` level  

You are given an integer `n`.

Return the **total** number of commas used when writing all integers from `[1, n]` (inclusive) in **standard** number formatting.

In **standard** formatting:

* A comma is inserted after **every three** digits from the right.
* Numbers with **fewer** than 4 digits contain no commas.

<br />

**Example 1:**
<pre>
<strong>Input:</strong> n = 1002
<strong>Output:</strong> 3
</pre>

**Explanation:**  
The numbers `"1,000"`, `"1,001"`, and `"1,002"` each contain one comma, giving a total of 3.

**Example 2:**
<pre>
<strong>Input:</strong> n = 998
<strong>Output:</strong> 0
</pre>

**Explanation:**  
All numbers from 1 to 998 have fewer than four digits. Therefore, no commas are used.

<br />

**Constraints:**

<code>1 <= n <= 10<sup>5</sup></code>

<br />

***

### Solution

**Time complexity:**  <code>O(1)</code>  
**Space complexity:**  <code>O(1)</code>  

**C++**

```C++
class Solution {
public:
  int countCommas(int n)
  {
    return max(0, n - 999);
  }
};
```