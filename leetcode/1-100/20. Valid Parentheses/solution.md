# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)  

`Easy` level 

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.  

An input string is valid if:  
  1. Open brackets must be closed by the same type of brackets.  
  2. Open brackets must be closed in the correct order.  
  3. Every close bracket has a corresponding open bracket of the same type.  

<br />

**Example 1:**

<pre>
<strong>Input:</strong> s = "()"  
<strong>Output:</strong> true  
</pre>

**Example 2:**

<pre>
<strong>Input:</strong> s = "()[]{}"  
<strong>Output:</strong> true  
</pre>

**Example 3:**

<pre>
<strong>Input:</strong> s = "(]"  
<strong>Output:</strong> false  
</pre>

**Example 4:**

<pre>
<strong>Input:</strong> s = "([])"  
<strong>Output:</strong> true  
</pre>

**Example 5:**

<pre>
<strong>Input:</strong> s = "([)]"  
<strong>Output:</strong> false  
</pre>

<br />

**Constraints:**

* <code>1 <= s.length <= 10<sup>4</sup></code>
* `s` consists of parentheses only `'()[]{}'`.

<br />

***

### Solution

<div style="border: 2px solid grey; border-radius: 8px; padding: 10px; font-size: 20px;">
  <a href="https://algobytes.net/blog/leetcode-20-solution/" target="_blank">For a deep-dive explanation of the solution with a step-by-step example, see here</a>
</div>

<br />

**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`  

<br />

**C++**

```cpp
class Solution {
public:
  bool isValid(string s) {
    stack<char> st;

    for(char c : s)
    {
      // Store opening brackets.
      if(c == '(' || c == '{' || c == '[')
      {
        st.push(c);
        continue;
      }

      // A closing bracket cannot be matched
      // if there is no opening bracket.
      if(st.empty()) return false;

      char top = st.top();

      // Check whether the closing bracket
      // matches the latest opening bracket.
      if((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')) 
      {
        return false;
      }

      // The pair is valid, remove the opening bracket.
      st.pop();
    }

    // No unmatched opening brackets should remain.
    return st.empty();
  }
};
```

**Java**

```java
class Solution {
  public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();

    for(char c : s.toCharArray()) {
      // Store opening brackets.
      if(c == '(' || c == '{' || c == '[') {
        stack.push(c);
        continue;
      }

      // A closing bracket cannot be matched
      // if there is no opening bracket.
      if(stack.isEmpty()) {
        return false;
      }

      char top = stack.peek();

      // Check whether the closing bracket
      // matches the latest opening bracket.
      if((c == ')' && top != '(') || (c == '}' && top != '{') || (c == ']' && top != '[')) {
        return false;
      }

      // The pair is valid, remove the opening bracket.
      stack.pop();
    }

    // No unmatched opening brackets should remain.
    return stack.isEmpty();
  }
}
```

**JavaScript**

```javascript
var isValid = function(s) {
    const stack = [];

    for(const c of s) {
      // Store opening brackets.
      if(c === '(' || c === '{' || c === '[') {
        stack.push(c);
        continue;
      }

      // A closing bracket cannot be matched
      // if there is no opening bracket.
      if(stack.length === 0) {
        return false;
      }

      const top = stack[stack.length - 1];

      // Check whether the closing bracket
      // matches the latest opening bracket.
      if((c === ')' && top !== '(') || (c === '}' && top !== '{') || (c === ']' && top !== '[')) {
        return false;
      }

      // The pair is valid, remove the opening bracket.
      stack.pop();
    }

    // No unmatched opening brackets should remain.
    return stack.length === 0;
};
```

**TypeScript**

```typescript
function isValid(s: string): boolean {
  const stack: string[] = [];

  for(const c of s) {
    // Store opening brackets.
    if(c === '(' || c === '{' || c === '[') {
      stack.push(c);
      continue;
    }

    // A closing bracket cannot be matched
    // if there is no opening bracket.
    if(stack.length === 0) {
      return false;
    }

    const top = stack[stack.length - 1];

    // Check whether the closing bracket
    // matches the latest opening bracket.
    if((c === ')' && top !== '(') || (c === '}' && top !== '{') || (c === ']' && top !== '[')) {
      return false;
    }

    // The pair is valid, remove the opening bracket.
    stack.pop();
  }

  // No unmatched opening brackets should remain.
  return stack.length === 0;
}
```

**Python**

```python
class Solution:
  def isValid(self, s: str) -> bool:
    stack = []

    for c in s:
      # Store opening brackets.
      if c in "({[":
        stack.append(c)
        continue

      # A closing bracket cannot be matched
      # if there is no opening bracket.
      if not stack:
        return False

      top = stack[-1]

      # Check whether the closing bracket
      # matches the latest opening bracket.
      if ((c == ')' and top != '(') or (c == '}' and top != '{') or (c == ']' and top != '[')):
        return False

      # The pair is valid, remove the opening bracket.
      stack.pop()

    # No unmatched opening brackets should remain.
    return not stack
```
