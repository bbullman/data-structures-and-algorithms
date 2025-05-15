# Khans algorithm

## Time Complexity
`O(V+E)`

## Space Complexity

At most, `O(V+E)`
I think is is optimal too in that you need to check all descendents in case there's a cycle, so you need to check at least `E`
For `V`, if they're all sources, this algorithm returns more or less immediately.  so upper bound on `v` in bigo.

## Strategy

1. Given a directed graph, store forward and back references as a map of adjacency **sets**
2. find the "source" nodes, those nodes which have outflowing references but no incoming references.  Basically `source_refs.keys() - back_refs.keys()`
3. Seed a FIFO queue (deque) of current sources with these global sources.
4. For each source popped from queue,
	1. add this to the partial solution of "sorted nodes"
	2. for each node this points to, remove the backreferences to this node
	3. If a child of source itself becomes a source from this backref removal, place it onto the FIFO queue
5. Once the queue of sources has been exhausted, we have a topological ordering if there remain no more back references.  Otherwise, cycles exist.
	1. Note that in the case of a multi graph, this algorithm will still find a topological sorting, but nodes in our topological ordering may be intermingled between disjoint graphs
	2. The topological sorting is not guaranteed to be unique

## Code (Python)
```python
from typing import List, Tuple
from collections import defaultdict, deque

def topo_sort(num_nodes:int, edges:List[Tuple[int,int]]) -> List[int]:
	adj_list = defaultdict(set)
	back_refs = defaultdict(set)
    for source, dest in edges:
		adj_list[source].add(dest)
		back_refs[dest].add(source)
    sources = deque(set(range(num_nodes)) - back_refs.keys())
	if not sources:
		raise TypeError("No detectable 'starting node' in graph")
	sorted_nodes = []
    while sources:
		source = sources.popleft()
		sorted_nodes.append(source)
		for dest in adj_list[source]:
			back_refs[dest].remove(source)
			if not back_refs[dest]:
				sources.append(dest)
				del back_refs[dest]
	if back_refs:
		raise TypeError("Cycle exists in graph")
	return sorted_nodes
```



# Examples

### Course schedule for college student (LC: Course Schedule II)

```python
from collections import defaultdict, deque

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        back_refs = defaultdict(int)
        forward_refs = defaultdict(set)
        for course, preq in prerequisites:
            forward_refs[preq].add(course)
            back_refs[course] += 1
        # seed anything that doesn't have a preq as a source    
        sources = deque(set(range(numCourses)) - back_refs.keys())
        topo_ordering = []
        while sources:
            source = sources.popleft()
            topo_ordering.append(source)
            # remember leaf nodes
            dependents = forward_refs.pop(source, set())
            for dependent in dependents:
                back_refs[dependent] -= 1
                if not back_refs[dependent]:
                    sources.append(dependent)
                    back_refs.pop(dependent)
        if back_refs:
            raise ValueError("Graph has cycles; we only support DAGs/DAG-forests")
        return topo_ordering            
        
        
    def findOrder_with_sets(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        back_refs = defaultdict(set)
        forward_refs = defaultdict(set)
        for course, preq in prerequisites:
            forward_refs[preq].add(course)
            back_refs[course].add(preq)
        # seed anything that doesn't have a preq as a source    
        sources = deque(set(range(numCourses)) - back_refs.keys())
        topo_ordering = []
        while sources:
            source = sources.popleft()
            topo_ordering.append(source)
            # remember leaf nodes
            dependents = forward_refs.pop(source, set())
            for dependent in dependents:
                back_refs[dependent].remove(source)
                if not back_refs[dependent]:
                    sources.append(dependent)
                    back_refs.pop(dependent)
        if back_refs:
            print(ValueError("Graph has cycles; we only support DAGs/DAG-forests"))
            return []
        return topo_ordering            
        
        
```




### Minimal Height Tree
```python
from collections import defaultdict, deque
import heapq

class Graph:
	def __init__(self):
		self.forward_refs = defaultdict(set)
		
	def add_connection(self, source, dest):
		self.forward_refs[source].add(dest)
		

class Solution:
    """
    Basically, this thing kind of "spirals inwards" from the leaves to the mht's
	even/odd parity means there's at most two innermost rootable tree nodes
    """
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if not edges:
            # Single node is a valid tree
            if n==1:
                return [n-1]
            elif n == 0:
                return []
            else:
                raise ValueError(f"Invalid value for {n} given {edges}")
        graph = Graph()
        for left, right in edges:
            graph.add_connection(left, right)
            graph.add_connection(right, left)
            
        # now that graph is wired, iterate through leafs
        frefs = graph.forward_refs
        # we could use a heap here but that's nlogn
        nodes = set(range(n))
        level_leaves = deque((
            (1, ref)
            for ref, edges in frefs.items()
            if len(edges) == 1
        ))
        if not level_leaves:
            # only valids
            raise ValueError(f"no leaf nodes detected => cycle exists") 
        seen = 0
        tree_roots = [node for _, node in level_leaves]
        best = 0 #max this
        # algorithm greedily consumes leaves, leaving biggest bois (distance wise) on the stack
        while level_leaves and seen < n-1:
            height, leaf  = level_leaves.popleft()
            seen += 1
            # should be len of 1, as leaves are leaves
            child = frefs[leaf].pop()
            if frefs[leaf]:
                raise ValueError(f"{leaf} wasn't a leaf after removing {child}")
            else:
                del frefs[leaf]
            frefs[child].remove(leaf)
            if len(frefs[child]) == 1:
                # might need backref/indegree here
                level_leaves.append((height+1, child))
                height += 1
                if height > best:
                    best = height
                    tree_roots = [child]
                elif height == best:
                    tree_roots.append(child)
                    
        return tree_roots
```

My suggestion was first to implement either a tree breadth first search, then expand it to graph breadth first search, then move up to actual topological sort
