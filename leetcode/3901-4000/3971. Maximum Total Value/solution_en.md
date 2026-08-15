# [3971. Maximum Total Value](https://leetcode.com/problems/maximum-total-value/description/)  

<code>Hard</code> level  

You are given two integer arrays <code>value</code> and <code>decay</code>, and an integer <code>m</code>. 
<li><code>value[i]</code> represents the initial value at index <code>i</code>.</li>
<li><code>decay[i]</code> represents how much the value decreases after each selection of index <code>i</code>.</li>  
<br/>
You may select any index <strong>multiple</strong> times. The total number of selections across all indices must not exceed <code>m</code>. 

<br />
If you select index <code>i</code> for the <code>t<sup>th<sup></code> time, where <code>t</code> is 1-indexed, the value gained is <code>value[i] - decay[i] * (t - 1)</code>.

<br />
Return the <strong>maximum</strong> total value you can obtain. Since the answer may be large, return it <strong>modulo</strong> <code>10<sup>9</sup> + 7</code>.

<br />

<strong>Example 1:</strong>  
<pre>
<strong>Input:</strong> value = [6,5,4], decay = [2,1,1], m = 4  
<strong>Output:</strong> 19  
</pre>
<strong>Explanation:</strong> 
<br />

One optimal sequence of selections is as follows:  
<li>By selecting index 0, the value gained is 6.</li>
<li>By selecting index 1, the value gained is 5.</li>
<li>By selecting index 2, the value gained is 4.</li>
<li>By selecting index 0 again, the value gained is <code>6 - 2 = 4</code>.</li>  
<br />
The total value is <code>6 + 5 + 4 + 4 = 19</code>. No other sequence of at most 4 selections gives a higher total value.

<br/>

<strong>Example 2:</strong>  
<pre>
<strong>Input:</strong> value = [7,2,2], decay = [3,2,1], m = 2  
<strong>Output:</strong> 11 
</pre>  
<strong>Explanation:</strong> 
<br />

One optimal sequence of selections is as follows:  
<li>By selecting index 0, the value gained is 7.</li>
<li>By selecting index 0 again, the value gained is <code>7 - 3 = 4</code>.</li> 
<br />
The total value is <code>7 + 4 = 11</code>.

<br/>

<strong>Example 3:</strong>  
<pre>
<strong>Input:</strong> value = [4,3], decay = [5,4], m = 5  
<strong>Output:</strong> 7 
</pre>  
<strong>Explanation:</strong> 
<br />

One optimal sequence of selections is as follows:  
<li>By selecting index 0, the value gained is 4.</li>
<li>By selecting index 1, the value gained is 3.</code>.</li> 
<br />
The total value is <code>4 + 3 = 7</code>.

<br/>
<strong>Constraints:</strong>

<br />
<li><code>1 <= value.length == decay.length <= 10<sup>5</sup></code></li>
<li><code>1 <= value[i], decay[i] <= 10<sup>9​</sup>​​​​​</code>​</li>
<li><code>1 <= m <= 10<sup>9</sup></code></li>  
<br />

***


<h3>Solution</h3>  

<strong>Time complexity:</strong> <code>O(m log n)</code>  
<strong>Space complexity:</strong> <code>O(n)</code>

<strong>C++</strong>  

```C++
class Solution {
public:
    static const long long MOD = 1000000007;

    long long countGE(vector<int>& value, vector<int>& decay, long long x) {
        long long cnt = 0;

        for (int i = 0; i < value.size(); i++) {
            if (value[i] < x) continue;

            if (decay[i] == 0) {
                cnt += 1000000000000000000LL;
            } else {
                cnt += (value[i] - x) / decay[i] + 1;
            }

            if (cnt > 4000000000000000000LL)
                return cnt;
        }

        return cnt;
    }

    int maxTotalValue(vector<int>& value, vector<int>& decay, int m) {
        long long low = 0;
        long long high = 0;

        for (int x : value)
            high = max(high, 1LL * x);

        long long threshold = 0;

        while (low <= high) {
            long long mid = (low + high) / 2;

            if (countGE(value, decay, mid) >= m) {
                threshold = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        long long ans = 0;
        long long taken = 0;

        for (int i = 0; i < value.size(); i++) {
            if (value[i] < threshold) continue;

            long long cnt;

            if (decay[i] == 0) {
                cnt = m - taken;
            } else {
                cnt = (value[i] - threshold) / decay[i] + 1;
            }

            taken += cnt;

            long long first = value[i];
            long long last = value[i] - decay[i] * (cnt - 1);

            long long sum = (first + last) * cnt / 2;

            ans = (ans + sum) % MOD;
        }

        while (taken > m) {
            ans = (ans - threshold + MOD) % MOD;
            taken--;
        }

        return ans % MOD;
    }
};
```