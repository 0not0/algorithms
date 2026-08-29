# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers)

**Time complexity:** `O(max(n, m))`  
**Space complexity:** `O(max(n, m))`  

`n` - the number of the nodes in `l1`  
`m` - the number of the nodes in `l2`  

```elixir
defmodule Solution do
  @spec add_two_numbers(l1 :: ListNode.t | nil, l2 :: ListNode.t | nil) :: ListNode.t | nil
  def add_two_numbers(l1, l2) do
    add(l1, l2, 0)
  end

  defp add(nil, nil, 0), do: nil

  defp add(l1, l2, carry) do
    val1 = if l1, do: l1.val, else: 0
    val2 = if l2, do: l2.val, else: 0

    sum = val1 + val2 + carry

    next1 = if l1, do: l1.next, else: nil
    next2 = if l2, do: l2.next, else: nil

    %ListNode{
      val: rem(sum, 10),
      next: add(next1, next2, div(sum, 10))
    }
  end
end
```