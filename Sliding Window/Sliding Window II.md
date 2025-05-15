* When you have a constraint such as k elements or sum, maximum, minimum, average.
* Subarrays
	* Number of 1s in bit string (Dynamic)
	* Timeframe (sliding)
	* Product Less than K (Fixed)

# Dynamic

* Define some variables for left, current, answer, and then use a loop with an iterator indicating the 'right' value
* Calculate the current value of the window
	* If value is greater than the constraint (or less than, whatever)
		* Decrease elements from the current calculation by removing from the left
		* Increase the left counter
	* Calculate answer via Math.Max(ans, right - left + 1);

```csharp
public int SlidingWindowDynamic(int[] nums, int k)
{
	int left = 0, curr = 0, ans = 0;
	for(int right = 0; right < nums.Length; right++)
	{
		curr += nums[right];
		while(curr > k)
		{
			curr -= nums[left];
			left++;
		}
		ans = Math.Max(ans, right - left + 1);
	}
	return ans;
}
```
# Fixed

* Define some variables for left, current, answer, and then use a loop to calculate the starting window. Stop when you reach the constraint.
* Then use a loop with an iterator indicating the 'right' value
* Set the current value of the window.
* Loop starting at the constraint until yo ureach the end of the array
	* Calculate the current value of the window
		* curr += nums at i minus nums at i - k
	* Calculate answer via Math.Max(ans, current value);
	* 
```csharp
public int SlidingWindowFixed(int[] nums, int k)
{
	int curr = 0;
    for (int i = 0; i < k; i++) {
        curr += nums[i];
    }

    int ans = curr;
    for (int i = k; i < nums.length; i++) {
        curr += nums[i] - nums[i - k];
        ans = Math.max(ans, curr);
    }

    return ans;
}
```