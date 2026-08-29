# [1. Two Sum](https://leetcode.com/problems/two-sum)   

`Easy level`

**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

**1. Without recursion**

```elixir
defmodule Solution do
  @spec two_sum(nums :: [integer], target :: integer) :: [integer]
  def two_sum(nums, target) do
    nums
    |> Enum.with_index()
    |> Enum.reduce_while(%{}, fn {num, i}, map ->
      val = target - num

      case Map.fetch(map, val) do
        {:ok, index} ->
          {:halt, [index, i]}

        :error ->
          {:cont, Map.put(map, num, i)}
      end
    end)
  end
end
```

**2. With recutsion**
```elixir
defmodule Solution do
  @spec two_sum(nums :: [integer], target :: integer) :: [integer]
  def two_sum(nums, target) do
    find(nums, target, %{}, 0)
  end

  defp find([num | rest], target, map, i) do
    val = target - num

    case Map.fetch(map, val) do
      {:ok, index} ->
        [index, i]

      :error ->
        find(rest, target, Map.put(map, num, i), i + 1)
    end
  end

  defp find([], _target, _map, _i), do: []
end
```