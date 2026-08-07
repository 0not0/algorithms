# [3984. Divisible Game](https://leetcode.com/problems/divisible-game/)  

<code>Medium</code> level 

You are given an integer array <code>nums</code> of length <code>n</code>.

Alice and Bob are playing a game. Alice chooses:

* An integer <code>k</code> such that <code>k > 1</code>.
* Two integers <code>l</code> and <code>r</code> such that <code>0 <= l <= r < n</code>.  

Initially, both Alice's and Bob's scores are 0.

For each index i in the range <code>[l, r]</code> (inclusive):

* If <code>nums[i]</code> is divisible by <code>k</code>, Alice's score **increases** by <code>nums[i]</code>.
* Otherwise, Bob's score **increases** by <code>nums[i]</code>.  
  
The **score difference** is Alice's score **minus** Bob's score.

Alice wants to **maximize** the score difference. If there are multiple values of <code>k</code> that achieve the **maximum** score difference, she chooses the **smallest** such <code>k</code>.

Return the **product** of the **maximum** score difference and the chosen value of <code>k</code>. Since the result can be large, return it **modulo** <code>10<sup>9</sup> + 7</code>.  
<br />

**Example 1:**
<pre>
<strong>Input:</strong> nums = [1,4,6,8]
<strong>Output:</strong> 36
</pre>
**Explanation:**

* Alice can choose <code>k = 2</code>, <code>l = 1</code>, and <code>r = 3</code>.
* All values in <code>nums[1..3]</code> are divisible by 2, so Alice's score is <code>4 + 6 + 8 = 18</code>, while Bob's score is 0.
* The score difference is 18, which is the maximum possible. Among all values of <code>k</code> that achieve this score difference, the smallest is 2.
* Therefore, the answer is <code>18 * 2 = 36</code>.  
<br />

**Example 2:**
<pre>
<strong>Input:</strong> nums = [2,1,2]
<strong>Output:</strong> 6
</pre>
**Explanation:**

* Alice can choose <code>k = 2</code>, <code>l = 0</code>, and <code>r = 2</code>.
* The values <code>nums[0]</code> and <code>nums[2]</code> are divisible by 2, so Alice's score is <code>2 + 2 = 4</code>. The value <code>nums[1]</code> is not divisible by 2, so Bob's score is 1.
* The score difference is <code>4 - 1 = 3</code>, which is the maximum possible. Among all values of k that achieve this score difference, the smallest is 2.
* Therefore, the answer is <code>3 * 2 = 6</code>.  
<br />

**Example 3:**
<pre>
<strong>Input:</strong> nums = [1]
<strong>Output:</strong> 1000000005
</pre>
**Explanation:**

* Alice must choose some <code>k > 1</code>. The smallest possible choice is <code>k = 2</code>.
* Since <code>nums[0]</code> is not divisible by 2, Alice's score is 0, while Bob's score is 1.
* The score difference is -1, which is the maximum possible.
* Therefore, the answer is <code>-1 * 2 = -2</code>. Modulo <code>10<sup>9</sup> + 7</code>, this equals 1000000005.  
<br /> 

**Constraints:**

* <code>1 <= nums.length <= 1000</code>
* <code>1 <= nums[i] <= 10<sup>6</sup></code>  

<br />

***  

### Solution  

**Time complexity:**  <code>O(n$\sqrt {M}$ + Dn)</code>  
**Space complexity:**  <code>O(D)</code>  
**where**:  
<code>M = max(nums)</code>  
<code> D </code> - number of different candidates <code>k</code>  
<code> n </code> - array size   

The algorithm consists of two phases:  
**1.** Collect all possible <code>k</code>: <code>O(n$\sqrt {M}$)</code>  
**2.** For each <code>k</code>, we traverse the array once: <code>O(Dn)</code>


**C++**
```C++
class Solution {
public:
  int divisibleGame(vector<int>& nums)
  {
    const long long MOD = 1e9 + 7;
    long long bestDiff = LLONG_MIN;
    int bestK = INT_MAX;

    unordered_set<int> ks;
    ks.insert(2);

    for (int x : nums)
    {
      for (int d = 2; 1LL * d * d <= x; ++d)
      {
        if (x % d == 0)
        {
          ks.insert(d);
          ks.insert(x / d);
        }
      }

      if (x > 1) ks.insert(x);
    }

    for (int k : ks)
    {
      long long cur = 0;
      long long best = LLONG_MIN;

      for (int x : nums)
      {
        long long val = (x % k == 0) ? x : -x;

        cur = max(val, cur + val);
        best = max(best, cur);
      }

      if (best > bestDiff || (best == bestDiff && k < bestK))
      {
        bestDiff = best;
        bestK = k;
      }
    }

    long long ans = (bestDiff % MOD) * bestK % MOD;

    if (ans < 0) ans += MOD;

    return ans;
  }
};
```