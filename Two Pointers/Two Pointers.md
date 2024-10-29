## Key Takeaways

* Best for traversing sequential data structures or vectors (arrays, lists)
* Typically involves two or more pointers moving in different or opposite directions
* Whenever a certain condition is met by one of the pointers, perform an operation

## Does this solution fit the Problem?

* Does the input data contain a linear data structure(s) (vector, array, list, string, etc.)?
* Can you process data elements at two different positions simultaneously?
* Can both pointers move independently of one another according to specific conditions or criteria, either in the same data structure or across data structures?
## Sample Problems

* **Palindrome**
	* **Problem:** Determine if a string is a palindrome or not
	* Start at both ends of the vector and move each pointer towards the center of the data
	* Compare each pointer's reference (value) and ensure they are the same
	* Return true if all elements match or false if otherwise
	* If the length of the vector is odd, make sure to account for that extra value (or ignore it)
* **Reversing an Array**
	* **Problem:** Reverse an Array in-place
	* Start at both ends of the vector and move each pointer towards the center of the data
	* Swap each pointer's reference (value) during iteration
	* If the length of the vector is odd, make sure to leave the center element in place
* **Two Sum (AKA: Pair with Given Sum)**
	* **Problem:** Given a sorted array of integers, find a pair in the array that sums to a number T (target, or K)
	* Start at both ends of the vector and move each pointer towards the center of the data
	* Compare the sum of both pointer's references (values) to the target value T
	* If it matches, return both values or indices
	* If it does not, move the right pointer first and compare again, then move the left pointer
* **Move all Specific Elements to End or Beginning of an Array**
	* **Problem:** Given an array of integers move all zeros to the end of an array
	* Start two pointers left and right at the start of the array
	* if the right pointer encounters a non-zero element, swap elements at the left and right position and increment both pointers
	* If right pointer encounters zero, increment right pointer only. Repeat until right pointer is at the end.
* **Three Sum**
	* **Problem:** Given a sorted array of integers, find three values in the array that sum to a number T
	* Use two pointers in each iteration. One at the leftmost element and the other at the rightmost element. Compare the sum with the first pointer chosen and increment or decrement accordingly.
	* Move the first pointer when the other two have exhausted all elements and if the target T has not been met by the sum