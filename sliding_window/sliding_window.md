# Sliding Window

[219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/description/?envType=problem-list-v2&envId=sliding-window)

This is a dynamic sliding window problem. I was previously stuck with this problem because I was trying to check every i and j to match the condition which are the limits of the sliding window, with the assumption that a one pass traversal of the entire array would contain every possible combination.

There is another less efficient way to solve this problem. Maintain a subarray of size k, in each iteration check if the newly added element is already there in the subarray. This is less time efficient and less memory efficient. 

```python
class Solution:
    def containsNearbyDuplicate(self, nums: list[int], k: int) -> bool:
        # maintain a map to capture the last known index of a number
        lastIndexMap = dict()

        for i in range(len(nums)):
            # having a previous occurence is a pre-requisite to the condition check
            if nums[i] in lastIndexMap:
                lastIndex = lastIndexMap[nums[i]]
                # this is the condition check
                if abs(i-lastIndex) <= k:
                    return True
            # update the map, we are only interested in the closest occurence
            lastIndexMap[nums[i]] = i
        return False
```
[594. Longest Harmonious Subsequence](https://leetcode.com/problems/longest-harmonious-subsequence/description/?envType=problem-list-v2&envId=sliding-window)

This is not a very efficient solution.

(!) TODO: Need to revisit this.

```python
class Solution:
    def findLHS(self, nums: list[int]) -> int:
        nums.sort()

        firstIndexOf = dict()
        maxLength = 0

        for i in range(len(nums)):

            minusOne = nums[i]-1
            if minusOne in firstIndexOf:
                maxLength = max(maxLength, i-firstIndexOf[minusOne]+1)
            
            if nums[i] not in firstIndexOf:
                firstIndexOf[nums[i]] = i
        
        return maxLength
```

[643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/description/?envType=problem-list-v2&envId=sliding-window)

This is a fixed window problem because the average needs to be calculated over a window of size k.

This is a single pass solution because we are first computing the sum of first k elements. After that we are traversing over element k -> n-1. 

```python
from functools import reduce

class Solution:
    def findMaxAverage(self, nums: list[int], k: int) -> float:
        i = 0
        j = k
        
        initialSum = reduce(lambda x, y: x + y, nums[:k], 0)
        maxSum = initialSum
        
        while j < len(nums):
            initialSum = initialSum + nums[j] - nums[i]
            maxSum = max(maxSum, initialSum)
            j += 1
            i += 1

        return maxSum/k
```

