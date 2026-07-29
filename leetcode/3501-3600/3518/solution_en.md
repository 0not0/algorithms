# [3518. Smallest Palindromic Rearrangement II](https://leetcode.com/problems/smallest-palindromic-rearrangement-ii)  

<code>Hard</code> level

***

### Solution

**Time complexity:**  <code>O(n<sup>2</sup>)</code>  
**Space complexity:**  <code>O(n)</code>  

**C++**

```C++
class Solution {
private:
  using int64 = long long;
  using int128 = __int128_t;

  int64 combination(int n, int r, int64 limit) {
    r = min(r, n - r);
    int128 result = 1;

    for (int i = 1; i <= r; ++i) {
      result = result * (n - r + i) / i;

      if (result >= limit) {
        return limit;
      }
    }

    return static_cast<int64>(result);
  }

  int64 countPermutations(const array<int, 26>& count, int64 limit) {
    int used = 0;
    int128 result = 1;

    for (int currentCount : count) {
      if (currentCount == 0) {
        continue;
      }

      int64 combinations = combination(used + currentCount, currentCount, limit);
      result *= combinations;

      if (result >= limit) {
        return limit;
      }

      used += currentCount;
    }

    return static_cast<int64>(result);
  }

public:
  string smallestPalindrome(string s, long long k) {
    array<int, 26> frequency{};
    array<int, 26> halfCount{};
    char middle = '\0';

    for (char character : s) {
      ++frequency[character - 'a'];
    }

    for (int i = 0; i < 26; ++i) {
      halfCount[i] = frequency[i] / 2;

      if (frequency[i] % 2 == 1) {
        middle = static_cast<char>('a' + i);
      }
    }

    if (countPermutations(halfCount, k) < k) return "";

    int halfLength = static_cast<int>(s.size()) / 2;
    string leftHalf;
    leftHalf.reserve(halfLength);

    for (int position = 0; position < halfLength; ++position) {
      for (int character = 0; character < 26; ++character) {
        if (halfCount[character] == 0) {
          continue;
        }

        --halfCount[character];
        int64 ways = countPermutations(halfCount, k);

        if (ways >= k) {
          leftHalf.push_back(static_cast<char>('a' + character));
          break;
        }

        k -= ways;
        ++halfCount[character];
      }
    }

    string rightHalf = leftHalf;
    reverse(rightHalf.begin(), rightHalf.end());

    if (middle != '\0') {
      return leftHalf + middle + rightHalf;
    }

    return leftHalf + rightHalf;
  }
};
```