## Solution
```python

from linked_list import LinkedList

def detect_cycle(head) -> bool:
  if not head:
    return False
  fast = head
  slow = head
  while fast:
    if fast.next:
      fast = fast.next.next
    else:
      fast = fast.next
    slow = slow.next
    if slow == None or fast == None:
      return False
    if fast == slow:
      return True
  return False

## Alternatively:

def detect_cycle(head) -> bool:
    if head is None:
        return False

    slow, fast = head, head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False
```

## Test Code

```python
def main():

    input = (
             [2, 4, 6, 8, 10, 12],
             [1, 3, 5, 7, 9, 11],
             [0, 1, 2, 3, 4, 6],
             [3, 4, 7, 9, 11, 17],
             [5, 1, 4, 9, 2, 3],
            )
    pos = [0, -1, 1, -1, 2]
    j = 1

    for i in range(len(input)):

        input_linked_list = LinkedList()
        input_linked_list.create_linked_list(input[i])
        print(f"{j}.\tInput: ", sep="", end="")
        if pos[i] == -1:
            print_list_with_forward_arrow(input_linked_list.head)
        else:
            print_list_with_forward_arrow_loop(input_linked_list.head)
        print("\n\tpos:", pos[i])
        if pos[i] != -1:
            length = input_linked_list.get_length(input_linked_list.head)
            last_node = input_linked_list.get_node(input_linked_list.head, length - 1)
            last_node.next = input_linked_list.get_node(input_linked_list.head, pos[i])

        print(f"\n\tDetected cycle = {detect_cycle(input_linked_list.head)}")
        j += 1
        print("-"*100, "\n")


if __name__ == "__main__":
    main()
```
# Complexity

This algorithm is simply Floyd's Tortoise and Hair or Floyd's Cycle-finding algorithm.

The naive approach involves a hashset. This is O(n) but requires O(n) space complexity.

**Time Complexity:** O(n) as we only make one pass over the array.
**Space Complexity:** O(1)
