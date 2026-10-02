# [22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)  

`Medium` level 

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*. 

<br />

**Example 1:**
<pre>
<strong>Input:</strong> n = 3
<strong>Output:</strong> ["((()))","(()())","(())()","()(())","()()()"]
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> n = 1
<strong>Output:</strong> ["()"]
</pre>

<br />

**Constraints:**

* `1 <= n <= 8`

<br />

***

### Solution

<div style="border: 2px solid grey; border-radius: 8px; padding: 10px; font-size: 20px;">
  <a href="https://algobytes.net/blog/leetcode-22-generate-parentheses-solution/" target="_blank">For a deep-dive explanation of the solution with a step-by-step example, see here</a>
</div>

<br />

**Time complexity:** <code>O(C<sub>n</sub> * n)</code>   
**Space complexity:** `O(n)`  

<br />

**C++**

```cpp
class Solution {
public:
  vector<string> generateParenthesis(int n) 
  {
    vector<string> result;
    string current;

    backtrack(n, 0, 0, current, result);

    return result;
  }

private:
  void backtrack(int n, int open, int close, string& current, vector<string>& result)
  {
    // A complete valid combination has 2 * n characters.
    if(current.size() == 2 * n)
    {
      result.push_back(current);

      return;
    }

    // Add '(' while we still have opening parentheses available.
    if(open < n) 
    {
      current.push_back('(');
      backtrack(n, open + 1, close, current, result);
      current.pop_back(); // Backtrack.
    }

    // Add ')' only when there is an unmatched '(' before it.
    if(close < open) 
    {
      current.push_back(')');
      backtrack(n, open, close + 1, current, result);
      current.pop_back(); // Backtrack.
    }
  }
};
```

**Java**

```java
class Solution {
  public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<>();
    StringBuilder current = new StringBuilder();

    backtrack(n, 0, 0, current, result);
    
    return result;
  }

  private void backtrack(int n, int open, int close, StringBuilder current, List<String> result) {
    // A complete valid combination has 2 * n characters.
    if(current.length() == 2 * n) {
      result.add(current.toString());

      return;
    }

    // Add '(' while we still have opening parentheses available.
    if(open < n) {
      current.append('(');
      backtrack(n, open + 1, close, current, result);
      current.deleteCharAt(current.length() - 1); // Backtrack.
    }

    // Add ')' only when there is an unmatched '(' before it.
    if(close < open) {
      current.append(')');
      backtrack(n, open, close + 1, current, result);
      current.deleteCharAt(current.length() - 1); // Backtrack.
    }
  }
}
```

**JavaScript**

```javascript
var generateParenthesis = function(n) {
  const result = [];

  const backtrack = (current, open, close) => {
    // A complete valid combination has 2 * n characters.
    if(current.length === 2 * n) {
      result.push(current);
      
      return;
    }

    // Add '(' while we still have opening parentheses available.
    if(open < n) {
      backtrack(current + '(', open + 1, close);
    }

    // Add ')' only when there is an unmatched '(' before it.
    if(close < open) {
      backtrack(current + ')', open, close + 1);
    }
  };

  backtrack('', 0, 0);

  return result;
};
```

**TypeScript**

```typescript
function generateParenthesis(n: number): string[] {
  const result: string[] = [];

  const backtrack = (current: string, open: number, close: number): void => {
    // A complete valid combination has 2 * n characters.
    if(current.length === 2 * n) {
      result.push(current);
      
      return;
    }

    // Add '(' while we still have opening parentheses available.
    if(open < n) {
      backtrack(current + '(', open + 1, close);
    }

    // Add ')' only when there is an unmatched '(' before it.
    if(close < open) {
      backtrack(current + ')', open, close + 1);
    }
  };

  backtrack('', 0, 0);

  return result;
};
```

**Python**

```python
class Solution:
  def generateParenthesis(self, n: int) -> List[str]:
    result = []
    current = []

    def backtrack(open_count: int, close_count: int) -> None:
      # A complete valid combination has 2 * n characters.
      if len(current) == 2 * n:
        result.append("".join(current))

        return

      # Add '(' while we still have opening parentheses available.
      if open_count < n:
        current.append("(")
        backtrack(open_count + 1, close_count)
        current.pop()  # Backtrack.

      # Add ')' only when there is an unmatched '(' before it.
      if close_count < open_count:
        current.append(")")
        backtrack(open_count, close_count + 1)
        current.pop()  # Backtrack.

    backtrack(0, 0)

    return result
```