# Bitwise

## [2683. Neighboring Bitwise XOR](https://leetcode.com/problems/neighboring-bitwise-xor/description/)


### Complexity
- Time complexity:
$O(n)$ since we only have to iterate through the dervied array once

- Space complexity:
 $O(1)$ since no extra space is required

### Code
```python []
from functools import reduce

class Solution:
    def doesValidArrayExist(self, derived: List[int]) -> bool:
        
        xorSum = reduce(lambda a, b: a^b, derived)

        return (xorSum == 0)
```