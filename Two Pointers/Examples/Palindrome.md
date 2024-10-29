```python
def is_palindrome(s) -> bool:
  left = 0
  right = len(s) - 1
  while left <= right:
    if s[left] != s[right]:
      return False
    else:
      left += 1
      right -= 1
  return True

def main():
    test_cases = ["RACECAR", "ABBA", "HellO", "FART"]
    i = 1
    for s in test_cases:
        print("Test Case #", i)
        print(is_palindrome(s))
        print("-" * 100, end="\n\n")
        i += 1

if __name__ == '__main__':
    main()
```

# Complexity

**Time Complexity:** O(n), note the algorithm will run n/2 times
**Space Complexity:** O(1), we are not allocating more than constant space