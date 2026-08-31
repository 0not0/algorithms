# [2058. Find the Minimum and Maximum Number of Nodes Between Critical Points](https://leetcode.com/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points)  

`Medium` level  

<br />

***

**Solution**  

**Time complexity:** <code>O(n)</code>  
**Space complexity:** <code>O(1)</code>

**C++** 
```C++
class Solution {
public:
  vector<int> nodesBetweenCriticalPoints(ListNode* head) {
    int first = -1;
    int last = -1;
    int minDistance = INT_MAX;

    ListNode* prev = head;
    ListNode* curr = head->next;

    int index = 1;

    while(curr->next)
    {
      bool critical =
        (curr->val > prev->val && curr->val > curr->next->val) ||
        (curr->val < prev->val && curr->val < curr->next->val);

      if(critical) 
      {
        if (first == -1) first = index;
        else minDistance = min(minDistance, index - last);

        last = index;
      }

      prev = curr;
      curr = curr->next;
      index++;
    }

    if(first == last) return {-1, -1};

    return {minDistance, last - first};
  }
};
```