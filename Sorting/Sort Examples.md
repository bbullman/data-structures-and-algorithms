Mostly useful in Lists that don't have a built in Sorting function or raw vectors/arrays, depending on the language.

Most of this is CS101/CS102 review. Things that have been lost to time. Reviewing this is hopefully optional, as any place that asks these sorts of questions above a junior-level is probably not worth working at as the implementation is rote and solved in most languages and therefore provides no business value.

However implementing these on custom vectors and array implementations is valid, although that scenario is incredibly rare.

## Insertion Sort

* **O(n^2)**
* Very similar to sliding window problem in that we shift by one across the vector surface and compare. This is the main reason that I have placed importance on it.

**Outer Loop:**
	1. Start the array at 1
	2. Set the current 'key' value to the current array index.
	3. Set the compared value 'flag' to the current array index - 1.
	
**Inner Loop:** 
	4. Process first two elements. Is element(0) < element(1)? If not, swap them.
	5. Process second set of elements: element(1) and element(2). If element(2) is less that element(1), swap them again. Compare element(1) backwards to element(0)...
	6. Repeat.
	
```csharp
public int[] InsertionSort(int[] array)
{
	for (int i = 1; i < array.Length; i++)
	{
		var key = array[i];
		var flag = 0;
		for (int j = i - 1; j >= 0 && flag != 1;)
		{
			if (key < array[j])
			{
				array[j + 1] = array[j];
				j--;
				array[j + 1] = key;
			}
			else 
			{
				flag = 1;
			}
		}
	}
	return array;
}
```

**Key Takeaways**
* Insertion Sort is slow, but because it has a move one step forward, move (potentially all) steps backwards approach, it's good to understand the nested loop structure. 
* The inner loop can be structured as a *while* loop instead of a *for* loop.

## Quick Sort 

* **O(nlog(n))**
* Uses the ***Divide & Conquer*** approach via a **pivot** value.
* Selecting the first, last, random, or median element of the array as the pivot is the best approach.
* Can be done recursively very effectively.

**Setup:**
* Use two iterators (i, j)
* Set a pivot based on criteria above.
1. Loop while (i <= j)
	1. while(array(i) < pivot) // value of index i is less than pivot, continue
		1. Increment i
	2. while(array(j) > pivot) // value of index j is greater than pivot, continue
		1. Decrement j
	3. if(i<=j)
		1. Set a temporary value
		2. Swap the value of array(i) and array(j)
		3. increment i, decrement j
2. Recurse
	1. if leftindex < j
		1. Quicksort(array, leftindex, j))
	2. if rightindex > i
		1. Quicksort(array, i, rightindex)

```csharp
public int[] QuickSortArray(int[] array, int leftIndex, int rightIndex)
{
	var i = leftIndex;
	var j = rightIndex;
	var pivot = array[leftIndex];
	while (i <= j)
	{
		while (array[i] < pivot)
		{
			i++;
		}
		while (array[j] > pivot)
		{
			j--;
		}
		if (i <= j)
		{
			int temp = array[i];
			array[i] = array[j];
			array[j] = temp;
			i++;
			j--;
		}
	}
	if (leftIndex < j)
		QuickSortArray(array, leftIndex, j);
	if (i < rightIndex)
		QuickSortArray(array, i, rightIndex);
	
	return array;
}
```

**Key Takeaways**:
* Quicksort is the default **Array.Sort()** in many programming languages. You probably won't have to implement it if there's a List<> implementation.
* The recursive aspect can be a bit tricky. Just remember to increment or decrement until you need to swap, then recurse afterwards.

## Merge Sort

* ***O(nlog(n))**
* Requires O(n) space to store the extra elements.
* Uses the ***Divide & Conquer*** approach via a **pivot** value.

1. Check if the array has one element. If it does, it means all the elements are sorted. 
2. Use recursion to divide the array into two halves until we can't divide it anymore. This means dividing down to the atomic element.
3. Merge the arrays into a new array whose values are sorted. This means creating a new array each time.

![[Pasted image 20230620182834.png]]
![[Pasted image 20230620182839.png]]
![[Pasted image 20230620182854.png]]
![[Pasted image 20230620182904.png]]

```csharp
public int[] MergeSort(int[] array, int left, int right)
{
	if (left < right)
	{
		int middle = left + (right - left) / 2;
		MergeSort(array, left, middle);
		MergeSort(array, middle + 1, right);
		MergeArray(array, left, middle, right);
	}
	return array;
}

public void MergeArray(int[] array, int left, int middle, int right)
{
	var leftArrayLength = middle - left + 1;
	var rightArrayLength = right - middle;
	var leftTempArray = new int[leftArrayLength];
	var rightTempArray = new int[rightArrayLength];

	int i, j;
	for (i = 0; i < leftArrayLength; ++i)
		leftTempArray[i] = array[left + i];
	for (j = 0; j < rightArrayLength; ++j)
		rightTempArray[j] = array[middle + 1 + j];
		
	i = 0;
	j = 0;
	int k = left;
	while (i < leftArrayLength && j < rightArrayLength)
	{
		if (leftTempArray[i] <= rightTempArray[j])
		{
		array[k++] = leftTempArray[i++];
		}
		else
		{
		array[k++] = rightTempArray[j++];
		}
	}
	while (i < leftArrayLength)
	{
		array[k++] = leftTempArray[i++];
	}
	while (j < rightArrayLength)
	{
		array[k++] = rightTempArray[j++];
	}
}
```

## Heap Sort

* O(nlog(n))
* ***Heap sort is a sorting algorithm that uses a binary heap data structure**. It works by first creating a binary heap from the elements that we need to sort.
* **Advantages:** In place sorting algorithm, meaning no extra space is required unlike merge sort.

1. **The heapify phase:** In this phase, we transform the input array into a max heap – a binary tree in which the value of each node is greater than or equal to the value of its children nodes. This can be done by starting at the last non-leaf node in the tree and working backward towards the root, ensuring that each node satisfies the max heap property.

2. **The sort phase:** In this phase, the max heap is repeatedly removed until only one element remains. This is done by swapping the root node with the last element in the heap, and then ensuring that the new root node satisfies the max heap property. This process is repeated until only one element remains in the heap.
   
![[Pasted image 20230620182709.png]]

```csharp
public int[] HeapSort(int[] array, int size)
{
	if (size <= 1)
		return array;
	for (int i = size / 2 - 1; i >= 0; i--)
	{
		MaxHeapify(array, size, i);
	}
	for (int i = size - 1; i >= 0; i--)
	{
		var tempVar = array[0];
		array[0] = array[i];
		array[i] = tempVar;
		MaxHeapify(array, i, 0);
	}
	return array;
}

static void MaxHeapify(int[] array, int size, int index)
{

	var largestIndex = index;
	var leftChild = 2 * index + 1;
	var rightChild = 2 * index + 2;
	if (leftChild < size && array[leftChild] > array[largestIndex])
	{
		largestIndex = leftChild;
	}
	if (rightChild < size && array[rightChild] > array[largestIndex])
	{
		largestIndex = rightChild;
	}
	if (largestIndex != index)
	{
		var tempVar = array[index];
		array[index] = array[largestIndex];
		array[largestIndex] = tempVar;
		MaxHeapify(array, size, largestIndex);
	}
}
