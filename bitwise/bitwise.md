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

## [2425. Bitwise XOR of all pairings](https://leetcode.com/problems/bitwise-xor-of-all-pairings/description/)

```python
class Solution:
    def xorAllNums(self, nums1: List[int], nums2: List[int]) -> int:
        ans = 0
        if len(nums2)%2 != 0:
            for num in nums1:
                ans ^= num
        
        if len(nums1)%2 != 0:
            for num in nums2:
                ans ^= num
        
        return ans
```