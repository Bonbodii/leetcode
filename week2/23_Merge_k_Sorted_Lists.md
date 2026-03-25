# [23] [Merge_k_Sorted_Lists]

## Code (C++)

```cpp
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        auto comp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
        priority_queue<ListNode*, vector<ListNode*>, decltype(comp)> pq(comp);
        for (auto list : lists) if (list) pq.push(list);
        
        ListNode dummy(0);
        ListNode* tail = &dummy;
        while (!pq.empty()) {
            tail->next = pq.top(); pq.pop();
            tail = tail->next;
            if (tail->next) pq.push(tail->next);
        }
        return dummy.next;
    }
};
```
## Acceptance Screen Shot
![alt text](image.png)