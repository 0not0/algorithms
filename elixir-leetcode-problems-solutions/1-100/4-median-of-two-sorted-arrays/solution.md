# [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)  

`Hard level` 

**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`  

```elixir
defmodule Solution do
  @spec find_median_sorted_arrays(nums1 :: [integer], nums2 :: [integer]) :: float
  def find_median_sorted_arrays(nums1, nums2) do
    total = length(nums1) + length(nums2)
    target = div(total, 2)

    find(nums1, nums2, 0, target, 0, 0, rem(total, 2))
  end

  defp find(a, b, i, target, prev, curr, odd?) when i > target do
    if odd? == 1 do
      curr * 1.0
    else
      (prev + curr) / 2.0
    end
  end

  defp find([], [b | bs], i, target, _prev, curr, odd?) do
    find([], bs, i + 1, target, curr, b, odd?)
  end

  defp find([a | as], [], i, target, _prev, curr, odd?) do
    find(as, [], i + 1, target, curr, a, odd?)
  end

  defp find([a | as] = list1, [b | bs] = list2, i, target, _prev, curr, odd?) do
    if a <= b do
      find(as, list2, i + 1, target, curr, a, odd?)
    else
      find(list1, bs, i + 1, target, curr, b, odd?)
    end
  end
end
```