
## Solution
```python
def find_repeated_sequences(sequence: str, k: int) -> set:
    left = 0
    unique, res = set(), set()
    if not sequence:
      return None
    for right in range(k, len(sequence)+1):
      if sequence[left:right] not in unique:
        unique.add(sequence[left:right])
      else:
        res.add(sequence[left:right])
      left+=1
    return res
```

## Test Code

```python
def main():
    inputs_string = ["ACGT", "AGACCTAGAC", "AAAAACCCCCAAAAACCCCCC", "GGGGGGGGGGGGGGGGGGGGGGGGG",
                     "TTTTTCCCCCCCTTTTTTCCCCCCCTTTTTTT", "TTTTTGGGTTTTCCA",
                     "AAAAAACCCCCCCAAAAAAAACCCCCCCTG", "ATATATATATATATAT"]
    inputs_k = [3, 3, 8, 12, 10, 14, 10, 6]

    for i in range(len(inputs_k)):
        print(i + 1, ".\tInput Sequence: \'", inputs_string[i], "\'", sep="")
        print("\tk: ", inputs_k[i], sep="")
        find_repeated_sequences(inputs_string[i], inputs_k[i])
        print("-"*100)


if __name__ == '__main__':
    main()
```

## Complexity

**Time Complexity:** k-length substrings is O(n-k+1)
* Hash or Add to Set: O(1)
**Space Complexity:** The hash set is O(n-k+1) strings, so O(n)