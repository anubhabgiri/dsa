# heap problems

### [3066. Minimum Operations to Exceed Threshold Value II](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii/description/)

```python
import heapq
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        
        # convert the list into a priority queue
        heapq.heapify(nums)

        operations = 0
        # operation can only be applied as long as 
        # there are 2 or more elements present
        while len(nums) >= 2:
            # pop the smallest element
            x = heapq.heappop(nums)
            # if x has reached boundary condition
            # we can break the loop as all subsequent elements will be gte k
            if x >= k:
                break
            y = heapq.heappop(nums)
            # add the compound element to the q
            heapq.heappush(nums, 2*x + y)
            # increment the operation count
            operations += 1
        return operations
```