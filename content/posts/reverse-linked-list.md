---
title: "Reverse a Linked List"
date: 2023-05-30
draft: false

tags: ['leetcode', 'linked list']
categories: ['LeetCode']
toc: true
---

# How to reverse a linked list
1. Initialize
    - null `prev`
    - `curr` node pointing to head
2. Change directions
    - save `curr`'s next into a variable `next`
    - point `curr`'s next pointer to `prev`
3. Move the `curr` and `prev` nodes one step ahead
    - `prev` becomes `curr`
    - `curr` becomes `next`
4. Repeat steps 2 and 3 until `curr` is `NULL`


{{< figure src="/images/reverse_linked_list.png" title="Infographic on Reversing a Linked List" >}}


# Code for reversing a linked list
## Python
```python
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
    prev = None
    curr = head
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node

    return prev
```

# Notes
1. I will be modifying the infographic to be more minimalistic. Maybe will think of doing a flashcard of all the important and frequent concepts required for passing the interviews.
2. The most important aspect of reversing a linked list is to remember to use a dummy null node at the beginning. It seems to be a re-occuring theme to initialize a dummy node in many linked list problems. I will try to find that pattern and write an article about it.