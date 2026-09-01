# [1. Two Sum](https://leetcode.com/problems/two-sum/description/)  

<code>Easy</code> level

Given an array of integers <code>nums</code> and an integer <code>target</code>, return <em>indices of the two numbers such that they add up to <code>target</code></em>.  
You may assume that each input would have <strong><em>exactly</em> one solution</strong>, and you may not use the same element twice.   
You can return the answer in any order.

<strong>Example 1:</strong>  
<pre>
<strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
<strong>Explanation:</strong> Because nums[0] + nums[1] == 9, we return [0, 1].
</pre>  

<strong>Example 2:</strong>  
<pre>
<strong>Input:</strong> nums = [3,2,4], target = 6
<strong>Output:</strong> [1,2]
</pre>  

<strong>Example 3:</strong>  
<pre>
<strong>Input:</strong> nums = [3,3], target = 6
<strong>Output:</strong> [0,1]
</pre>  

<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= target &lt;= 10<sup>9</sup></code></li>
	<li><strong>Only one valid answer exists.</strong></li>
</ul>  

<strong>Follow-up:</strong> Can you come up with an algorithm that is less than <code>O(n<sup>2</sup>)</code> time complexity?

***  

Розв'язування  

<strong>Два цикла <code>for</code></strong>  
Рішення, гарне по Space complexity, але погане по Time complexety.  
Space complexity: O(1)  
Time complexity: O(n<sup>2</sup>)  

#### JavaScript
```js
const twoSum = (nums, target) => {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
}
```  

Використання <strong>Hash Map</strong>.  
Покращує Time complexity, але погіршує Space complexity:   
Space complexity: O(n)  
Time complexity: O(n)
#### JavaScript

```js
const twoSum = (nums, target) => {
  const obj = {};

  for(let i = 0; i < nums.length; i++) {
      let val = target - nums[i];

      if(val in obj) {
          return [obj[val], i];
      } else {
          obj[nums[i]] = i;
      }
  }
}
```  
#### C++
```C++
class Solution {
public:
  vector<int> twoSum(vector<int>& nums, int target) {
    std::unordered_map<int, int> map;
  
    for(int i = 0; i < nums.size(); i++) 
    {
      int val = target - nums.at(i);
          
      auto it = map.find(val);
          
      if(it != map.end())
      {
          return {it->second, i};
      } else
      {
          map[nums[i]] = i;
      }
    }
    
    return {};
  }
};
```
**C**  
```c
#define HASH_SIZE 20011

typedef struct {
  int key;
  int index;
  int used;
} Entry;

int hash(int key) {
  unsigned int x = (unsigned int)key;
  return x % HASH_SIZE;
}

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
  Entry table[HASH_SIZE] = {0};

  for(int i = 0; i < numsSize; i++) {
    int complement = target - nums[i];
    int h = hash(complement);

    while(table[h].used) {
      if(table[h].key == complement) {
        int* result = malloc(2 * sizeof(int));

        result[0] = table[h].index;
        result[1] = i;

        *returnSize = 2;
        return result;
      }

      h = (h + 1) % HASH_SIZE;
    }

    h = hash(nums[i]);

    while(table[h].used) {
        h = (h + 1) % HASH_SIZE;
    }

    table[h].key = nums[i];
    table[h].index = i;
    table[h].used = 1;
  }

  *returnSize = 0;

  return NULL;
}
```

**Java**
```java
class Solution {
  public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();

    for(int i = 0; i < nums.length; i++) {
      int val = target - nums[i];

      Integer index = map.get(val);

      if(index != null) return new int[]{index, i};

      map.put(nums[i], i);
    }

    return new int[]{};
  }
}
```

**Python3**
```python
class Solution:
  def twoSum(self, nums: List[int], target: int) -> List[int]:
    seen = {}

    for i, num in enumerate(nums):
        val = target - num

        if val in seen:
          return [seen[val], i]

        seen[num] = i

    return []
```

**TypeScript**
```typescript
function twoSum(nums: number[], target: number): number[] {
    const map = new Map<number, number>();

  for(let i = 0; i < nums.length; i++) {
    const val = target - nums[i];

    if(map.has(val)) return [map.get(val)!, i];

    map.set(nums[i], i);
  }

  return [];
};
```

**C#**
```c#
public class Solution
{
  public int[] TwoSum(int[] nums, int target)
  {
    var map = new Dictionary<int, int>();

    for(int i = 0; i < nums.Length; i++)
    {
      int val = target - nums[i];

      if(map.TryGetValue(val, out int index)) return new int[] { index, i };
      
      map[nums[i]] = i;
    }

    return Array.Empty<int>();
  }
}
```

**Go**
```go
func twoSum(nums []int, target int) []int {
  seen := make(map[int]int)

  for i, num := range nums {
    val := target - num

    if index, ok := seen[val]; ok {
      return []int{index, i}
    }

    seen[num] = i
  }

  return []int{}
}
```

**Kotlin**
```kotlin
class Solution {
  fun twoSum(nums: IntArray, target: Int): IntArray {
    val map = HashMap<Int, Int>()

    for (i in nums.indices) {
      val value = target - nums[i]

      if (map.containsKey(value)) {
        return intArrayOf(map[value]!!, i)
      }

      map[nums[i]] = i
    }

    return intArrayOf()
  }
}
```

**Swift**
```swift
class Solution {
  func twoSum(_ nums: [Int], _ target: Int) -> [Int] {
    var map = [Int: Int]()

    for i in 0..<nums.count {
      let value = target - nums[i]

      if let index = map[value] {
        return [index, i]
      }

      map[nums[i]] = i
    }

    return []
  }
}
```

**Rust**
```rust
use std::collections::HashMap;

impl Solution {
  pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
    let mut map = HashMap::new();

    for (i, &num) in nums.iter().enumerate() {
      let value = target - num;

      if let Some(&index) = map.get(&value) {
          return vec![index as i32, i as i32];
      }

      map.insert(num, i);
    }

    vec![]
  }
}
```

**Ruby**
```ruby
def two_sum(nums, target)
  map = {}

  nums.each_with_index do |num, i|
    value = target - num

    if map.key?(value)
      return [map[value], i]
    end

    map[num] = i
  end

  []
end
```

**PHP**
```php
class Solution
{
  function twoSum($nums, $target)
  {
    $map = [];

    foreach ($nums as $i => $num) {
      $value = $target - $num;

      if (array_key_exists($value, $map)) {
        return [$map[$value], $i];
      }

      $map[$num] = $i;
    }

    return [];
  }
}
```

**Dart**
```dart
class Solution {
  List<int> twoSum(List<int> nums, int target) {
    final Map<int, int> map = {};

    for (int i = 0; i < nums.length; i++) {
      final int value = target - nums[i];

      if (map.containsKey(value)) {
        return [map[value]!, i];
      }

      map[nums[i]] = i;
    }

    return [];
  }
}
```

**Scala**
```scala
import scala.collection.mutable

object Solution {
  def twoSum(nums: Array[Int], target: Int): Array[Int] = {
    val map = mutable.HashMap[Int, Int]()
    var i = 0

    while (i < nums.length) {
      val value = target - nums(i)

      map.get(value) match {
        case Some(index) =>
          return Array(index, i)

        case None =>
          map(nums(i)) = i
      }

      i += 1
    }

    Array()
  }
}
```