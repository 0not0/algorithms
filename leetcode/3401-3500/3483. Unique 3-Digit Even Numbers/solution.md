# [3483. Unique 3-Digit Even Numbers](https://leetcode.com/problems/unique-3-digit-even-numbers/)

`Easy` level  

You are given an array of digits called `digits`. Your task is to determine the number of **distinct** three-digit even numbers that can be formed using these digits.

**Note:** Each copy of a digit can only be used **once per number**, and there may not be leading zeros.  

<br />

**Example 1:**
<pre>
<strong>Input:</strong> digits = [1,2,3,4]
<strong>Output:</strong> 12
<strong>Explanation:</strong> The 12 distinct 3-digit even numbers that can be formed are 124, 132, 134, 142, 214, 234, 312, 314, 324, 342, 412, and 432. Note that 222 cannot be formed because there is only 1 copy of the digit 2.
</pre>

**Example 2:**
<pre>
<strong>Input:</strong> digits = [0,2,2]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The only 3-digit even numbers that can be formed are 202 and 220. Note that the digit 2 can be used twice because it appears twice in the array.
</pre>

**Example 3:**
<pre>
<strong>Input:</strong> digits = [6,6,6]
<strong>Output:</strong> 1
<strong>Explanation:</strong> Only 666 can be formed.
</pre>

**Example 4:**
<pre>
<strong>Input:</strong> digits = [1,3,5]
<strong>Output:</strong> 0
<strong>Explanation:</strong> No even 3-digit numbers can be formed.
</pre> 

<br />

**Constraints:**

* `3 <= digits.length <= 10`
* `0 <= digits[i] <= 9`  

<br />

***

### Solution

**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`  

**C++**

```cpp
class Solution {
public:
  int totalNumbers(vector<int>& digits) {
    int count[10] = {};
    int res = 0;

    for(int d : digits) count[d]++;

    for(int num = 100; num <= 998; num += 2)
    {
      int a = num / 100;
      int b = (num / 10) % 10;
      int c = num % 10;

      int need[10] = {};
      need[a]++;
      need[b]++;
      need[c]++;

      bool possible = true;

      for(int d = 0; d < 10; d++)
      {
        if(need[d] > count[d])
        {
          possible = false;
          break;
        }
      }

      if(possible) res++;
    }

    return res;
  }
};
```

**Java**

```java
class Solution {
  public int totalNumbers(int[] digits) {
    int[] count = new int[10];

    for(int d : digits) count[d]++;

    int res = 0;

    for(int num = 100; num <= 998; num += 2) {
      int a = num / 100;
      int b = (num / 10) % 10;
      int c = num % 10;

      int[] need = new int[10];
      need[a]++;
      need[b]++;
      need[c]++;

      boolean possible = true;

      for(int d = 0; d < 10; d++) {
        if(need[d] > count[d]) {
          possible = false;
          break;
        }
      }

      if(possible) res++;
    }

    return res;
  }
}
```

**JavaScript**

```javascript
var totalNumbers = function(digits) {
  const count = new Array(10).fill(0);

  for(const d of digits) count[d]++;

  let res = 0;

  for(let num = 100; num <= 998; num += 2) {
    const a = Math.floor(num / 100);
    const b = Math.floor(num / 10) % 10;
    const c = num % 10;

    const need = new Array(10).fill(0);
    need[a]++;
    need[b]++;
    need[c]++;

    let possible = true;

    for(let d = 0; d < 10; d++) {
      if(need[d] > count[d]) {
        possible = false;
        break;
      }
    }

    if(possible) res++;
  }

  return res;
};
```

**TypeScript**

```typescript
function totalNumbers(digits: number[]): number {
  const count: number[] = new Array(10).fill(0);

  for(const d of digits) count[d]++;

  let res = 0;

  for(let num = 100; num <= 998; num += 2) {
    const a = Math.floor(num / 100);
    const b = Math.floor(num / 10) % 10;
    const c = num % 10;

    const need: number[] = new Array(10).fill(0);
    need[a]++;
    need[b]++;
    need[c]++;

    let possible = true;

    for(let d = 0; d < 10; d++) {
      if(need[d] > count[d]) {
        possible = false;
        break;
      }
    }

    if(possible) res++;
  }

  return res;
}
```

**Python**

```python
class Solution:
  def totalNumbers(self, digits: List[int]) -> int:
    count = [0] * 10

    for d in digits:
      count[d] += 1

    res = 0

    for num in range(100, 999, 2):
      a = num // 100
      b = (num // 10) % 10
      c = num % 10

      need = [0] * 10
      need[a] += 1
      need[b] += 1
      need[c] += 1

      possible = True

      for d in range(10):
        if need[d] > count[d]:
          possible = False
          break

      if possible: 
          res += 1

    return res
```