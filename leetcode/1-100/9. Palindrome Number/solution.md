# [9. Palindrome Number](https://leetcode.com/problems/palindrome-number)  

`Easy` level  

Given an integer `x`, return `true` if `x` is a **palindrome**<sup>1</sup>, and `false` otherwise.  

**1.** An integer is a **palindrome** when it reads the same forward and backward.  
For example, `121` is a palindrome while `123` is not.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> x = 121
<strong>Output:</strong> true
<strong>xplanation:</strong> 121 reads as 121 from left to right and from right to left.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> x = -121
<strong>Output:</strong> false
<strong>Explanation:</strong> From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> x = 10
<strong>Output:</strong> false
<strong>Explanation:</strong> Reads 01 from right to left. Therefore it is not a palindrome.
</pre>

**Constraints:**

* <code>-2<sup>31</sup> <= x <= 2<sup>31</sup> - 1</code>  

<br />

**Follow up:** Could you solve it without converting the integer to a string?  

***

**Solution**  

**Time complexity:** <code>O(log(x))</code>  
**Space complexity:** <code>O(1)</code>

**C++**  
```C++
class Solution 
{
  public:
    bool isPalindrome(int x)
    {
      if(x < 0 || (x && x % 10 == 0)) return false;
          
      int rev = 0;

      while(x > rev)
      {
        rev = rev * 10 + x % 10;
        x /= 10;
      }

      return x == rev || x == rev / 10;
    }
};
```
 
**Java**  
### First solution

```java
class Solution {
  public boolean isPalindrome(int x) {
    String v = String.valueOf(x);
    StringBuilder newV = new StringBuilder();
    int length  = v.length();

    for(int i = length - 1; i >= 0; i--) newV.append(v.charAt(i));

    return v.equals(newV.toString());
  }
}
```

### Second solution
```java
class Solution {
  public boolean isPalindrome(int x) {
    if (x < 0 || (x % 10 == 0 && x != 0)) return false;

    int reversedHalf = 0;

    while(x > reversedHalf) {
        reversedHalf = reversedHalf * 10 + x % 10;
        x /= 10;
    }

    return x == reversedHalf || x == reversedHalf / 10;
  }
}
```