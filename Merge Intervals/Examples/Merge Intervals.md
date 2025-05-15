
## Solution

```python
def merge_intervals(intervals) -> list:
    if not intervals:
      return None
    if len(intervals) == 1:
      return intervals
    res = []
    res.append(intervals[0]) 
    curr = 0
    for a, b in intervals:
        start, end = res[curr]
        if a <= end:
            if b >= end:
              res[curr] = (start, b)
        elif a >= end:
            res.append((a,b))
            curr += 1
        prev = b
    return res
```

## Solution 2

```python
def merge_intervals(intervals):
    if not intervals:
        return None
    result = []
    result.append([intervals[0][0], intervals[0][1]])
    for i in range(1, len(intervals)):
        last_added_interval = result[len(result) - 1]
        cur_start = intervals[i][0]
        cur_end = intervals[i][1]
        prev_end = last_added_interval[1]
        
        if cur_start <= prev_end:
            result[-1][1] = max(cur_end, prev_end)
        else:
            result.append([cur_start, cur_end])
    return result
```
## Test Code

```python 
def main():
    intervals =  [[15,96],[35,50],[38,47],[43,45],[44,94]]
	print(f'Input Interval list:{intervals}')
	print(f'Merged Intervals:'{merge_intervals(intervals)}')
    
    all_intervals = [
    [[1, 5], [3, 7], [4, 6]],
    [[1, 5], [4, 6], [6, 8], [11, 15]],
    [[3, 7], [6, 8], [10, 12], [11, 15]],
    [[1, 5]],
    [[1, 9], [3, 8], [4, 4]],
    [[1, 2], [3, 4], [8, 8]],
    [[1, 5], [1, 3]],
    [[1, 5], [6, 9]],
    [[0, 0], [1, 18], [1, 3]]
    ]

    for i in range(len(all_intervals)):
        print(i + 1, ". Intervals to merge: ", all_intervals[i], sep="")
        result = merge_intervals(all_intervals[i])
        print("-"*100)

if __name__ == '__main__':
    main()
```

## Complexity

**Time Complexity:** O(n) we make one pass across the interval array of tuples
**Space Complexity:** O(1), but we have to allocate another output array or list of tuples which can be equal to the input if there are no overlapping intervals. The output isn't normally counted against Space Complexity here.