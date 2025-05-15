# Basic Approach

* Arbitrary node starting point.
* Array needed to mark nodes as visited.
* Stack needed to handle nodes that need to be processed.
* Marking nodes is mandatory. Processing nodes is optional.
* For each transition or edge on the node, if neighbor is not visited, recurse.

# Main Process

```
procedure DFS(node):
    mark node as visited
    process(node)
    
    for each neighbor in node.neighbors:
        if neighbor is not visited:
            DFS(neighbor)
```

Follow the below method to implement DFS traversal.

1. Create a set or array to keep track of visited nodes.
2.  Choose a starting node.
3.  Create an empty stack and push the starting node onto the stack.
4.  Mark the starting node as visited.
5.  While the stack is not empty, do the following:
	* Pop a node from the stack.
	* Process or perform any necessary operations on the popped node.
	* Get all the adjacent neighbors of the popped node.
	* For each adjacent neighbor, if it has not been visited, do the following:
	* Mark the neighbor as visited.
	* Push the neighbor onto the stack.
6. Repeat step 5 until the stack is empty.
