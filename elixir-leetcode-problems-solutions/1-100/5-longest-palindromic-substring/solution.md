# [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring) 

`Medium level`  

**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`  

```elixir
defmodule Solution do
  @spec longest_palindrome(s :: String.t()) :: String.t()
  def longest_palindrome(s) do
    chars = :binary.bin_to_list(s)

    transformed =
      [:sep | Enum.flat_map(chars, fn c -> [c, :sep] end)]
      |> List.to_tuple()

    n = tuple_size(transformed)
    p = :array.new(n, default: 0)

    {p, _center, _right, best_center, best_len} =
      manacher(transformed, p, n, 0, 0, 0, 0, 0)

    start = div(best_center - best_len, 2)

    binary_part(s, start, best_len)
  end

  defp manacher(_t, p, n, i, center, right, best_center, best_len)
       when i >= n do
    {p, center, right, best_center, best_len}
  end

  defp manacher(t, p, n, i, center, right, best_center, best_len) do
    mirror = 2 * center - i

    radius =
      if i < right and mirror >= 0 do
        min(right - i, :array.get(mirror, p))
      else
        0
      end

    radius = expand(t, n, i, radius)

    p = :array.set(i, radius, p)

    {center, right} =
      if i + radius > right do
        {i, i + radius}
      else
        {center, right}
      end

    {best_center, best_len} =
      if radius > best_len do
        {i, radius}
      else
        {best_center, best_len}
      end

    manacher(
      t,
      p,
      n,
      i + 1,
      center,
      right,
      best_center,
      best_len
    )
  end

  defp expand(t, n, center, radius) do
    left = center - radius - 1
    right = center + radius + 1

    if left >= 0 and right < n and elem(t, left) == elem(t, right) do
      expand(t, n, center, radius + 1)
    else
      radius
    end
  end
end
```