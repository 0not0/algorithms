# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)  

`Medium level`

**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`  

**1.**  
```elixir
defmodule Solution do
  @spec length_of_longest_substring(s :: String.t()) :: integer
  def length_of_longest_substring(s) do
    solve(s, %{}, 0, 0, 0)
  end

  defp solve(<<>>, _last, _right, _left, best), do: best

  defp solve(<<c, rest::binary>>, last, right, left, best) do
    left = max(left, Map.get(last, c, -1) + 1)

    solve(
      rest,
      Map.put(last, c, right),
      right + 1,
      left,
      max(best, right - left + 1)
    )
  end
end
```

**2.**
```elixir
defmodule Solution do
  @spec length_of_longest_substring(s :: String.t()) :: integer
  def length_of_longest_substring(s) do
    result = solve(s, 0, 0, 0)

    for c <- 0..255 do
      Process.delete(c)
    end

    result
  end

  defp solve(<<>>, _right, _left, best), do: best

  defp solve(<<c, rest::binary>>, right, left, best) do
    prev = Process.get(c, -1)

    left = max(left, prev + 1)

    Process.put(c, right)

    solve(
      rest,
      right + 1,
      left,
      max(best, right - left + 1)
    )
  end
end
```