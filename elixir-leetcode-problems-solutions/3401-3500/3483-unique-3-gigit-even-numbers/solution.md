# [3483. Unique 3-Digit Even Numbers](https://leetcode.com/problems/unique-3-digit-even-numbers/description/)  

`Easy level`

> If you want to check the solutions in C++, Java, Python, JavaScript, or TypeScript and compare them with the Elixir solution, [see here](https://algobytes.net/blog/leetcode-3483-solution/)


**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`  

```elixir
defmodule Solution do
  @spec total_numbers(digits :: [integer]) :: integer
  def total_numbers(digits) do
    count =
      Enum.reduce(digits, %{}, fn d, acc ->
        Map.update(acc, d, 1, &(&1 + 1))
      end)

    Enum.count(100..998//2, fn num ->
      a = div(num, 100)
      b = rem(div(num, 10), 10)
      c = rem(num, 10)

      need =
        [a, b, c]
        |> Enum.frequencies()

      Enum.all?(need, fn {d, required} ->
        required <= Map.get(count, d, 0)
      end)
    end)
  end
end
```