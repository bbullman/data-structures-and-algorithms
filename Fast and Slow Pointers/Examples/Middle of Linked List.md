```python
from linked_list import LinkedList
from linked_list_node import LinkedListNode

def get_middle_node(head) -> LinkedListNode:
    slow, fast = head, head
    if head is None or head.next is None:
      return head
    
    while fast and fast.next:
      slow = slow.next
      fast = fast.next.next
    return slow
```

## Test Code

```python
def main():

    input = (
        [1, 2, 3, 4, 5],
        [1, 2, 3, 4, 5, 6],
        [3, 2, 1],
        [10],
        [1, 2],
    )

    for i in range(len(input)):
        input_linked_list = LinkedList()
        input_linked_list.create_linked_list(input[i])
        print(i+1, ".\tLinked list: ", sep="", end="")
        print_list_with_forward_arrow(input_linked_list.head)
        print("\n\tMiddle of the linked list: ",
              get_middle_node(input_linked_list.head).data)
        print("-"*100, "\n")

if __name__ == "__main__":
    main()
```
## Complexity

Naive approach uses an external array to store elements of the LinkedList and checks the middle index value.

**Time Complexity:** O(n) since we traverse the list once
**Space Complexity:** O(1) since we do not allocate any extra space for this.