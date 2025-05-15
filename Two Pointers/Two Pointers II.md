1. Require moving two pointers along an array or two arrays as input.

# Single Array

* Start at front and back of array

```csharp
i = 0; 
j = arr.Length - 1;
while ( i < j ) // or equal
{
	Do something
	i++;
	j--;
}
```

# Two Arrays

* Start at front of both arrays
* While loop over the arrays
```csharp
	while
	(i < arr1.Length && j < arr2.Length)
	{
		Do Something
		i++;
		j++;
	}
while(i < arr1.length)
{
	Do something to exhaust
	i++;
}
while (j < arr2.length)
{
	Do something to exhaust
	j++;
}
return ans;