# [3986. Number of Elapsed Seconds Between Two Times](https://leetcode.com/problems/number-of-elapsed-seconds-between-two-times/)  

<code>Easy</code> level 

You are given two valid times <code>startTime</code> and <code>endTime</code>, each represented as a string in the format <code>"HH:MM:SS"</code>.

Return the number of seconds that have elapsed from <code>startTime</code> to <code>endTime</code>.  
<br />
**Example 1:**
<pre>
<strong>Input:</strong> startTime = "01:00:00", endTime = "01:00:25"
<strong>Output:</strong> 25
</pre>
**Explanation:**

<code>endTime</code> is 25 seconds ahead of <code>startTime</code>.  

**Example 2:**
<pre>
<strong>Input:</strong> startTime = "12:34:56", endTime = "13:00:00"
<strong>Output:</strong> 1504
</pre>
**Explanation:**

<code>endTime</code> is 25 minutes and 4 seconds ahead of <code>startTime</code>, which equals 1504 seconds.  

<br />

**Constraints:**

* <code>startTime.length == 8</code>
* <code>endTime.length == 8</code>
* <code>startTime</code> and <code>endTime</code> are valid times in the format <code>"HH:MM:SS"</code>
* <code>00 <= HH <= 23</code>
* <code>00 <= MM <= 59</code>
* <code>00 <= SS <= 59</code>
* <code>endTime</code> is not earlier than <code>startTime</code> 

<br />

***  

### Solution

**Time complexity:** <code>O(1)</code>  
**Space complexity:** <code>O(1)</code>  

**C++**
```C++
class Solution
{
  public:
    int secondsBetweenTimes(string startTime, string endTime)
    {
      auto seconds = [](const string& t)
      {
        return ((t[0] - '0') * 10 + t[1] - '0') * 3600
            + ((t[3] - '0') * 10 + t[4] - '0') * 60
            + ((t[6] - '0') * 10 + t[7] - '0');
      };

      return seconds(endTime) - seconds(startTime);
    }
};
```