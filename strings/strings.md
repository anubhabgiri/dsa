# String manipulation

### Leetcode 3223. Minimum Length of String After Operations

```python
class Solution:
    def minimumLength(self, s: str) -> int:
        # Create a frequency array of all letters
        letterCount = [0]*26
        for c in s:
            letterCount[ord(c) - ord('a')] += 1

        total = len(s)
        
        # Iterate through each letter frequency
        for count in letterCount:
            # no operation is possible if count is less than 3
            if count < 3:
                continue
            
            else:
                # If initial count is even then 2 will always remain else 1
                if count%2 == 0:
                    total -= (count-2)
                else:
                    total -= (count-1)

        return total

```