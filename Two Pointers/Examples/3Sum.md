```python
def three_sum(nums, target) -> bool:
  nums.sort() # O(nlogn) # Also works: nums = sorted(nums) 
  i = 0
  left = 1
  right = len(nums) - 1
  for i in range(len(nums) - 2): # O(n - 2)
    while left < right: # O(n - 2)
      sum = nums[i] + nums[left] + nums[right]
      if sum == target:
        return True
      if sum < target:
        left += 1
      elif sum > target:
        right -= 1
    left = i+1
    right = len(nums) - 1
  return False
  
def main():
    nums_lists = [[3, 7, 1, 2, 8, 4, 5],
                  [-1, 2, 1, -4, 5, -3],
                  [2, 3, 4, 1, 7, 9],
                  [1, -1, 0],
                  [2, 4, 2, 7, 6, 3, 1]]

    targets = [10, 7, 20, -1, 8]

    for i in range(len(nums_lists)):
        print(i + 1, ".\tInput array: ", nums_lists[i], sep="")
        if three_sum(nums_lists[i], targets[i]):
            print("\tSum for", targets[i], "exists")
        else:
            print("\tSum for", targets[i], "does not exist")
        print("-"*100)

if __name__ == '__main__':
    main()
```

## Complexity

**Time Complexity:** O(nlogn n^2) = O(n^2), the outer and inner loop require us to go through the solution twice or O(n) * O(n-2) times.
**Space Complexity:** O(1), we do not allocate extra space
