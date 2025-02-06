# Array

### [1726. Tuple with Same Product](https://leetcode.com/problems/tuple-with-same-product/description/)

```python
class Solution:
    def tupleSameProduct(self, nums: List[int]) -> int:
        graph = defaultdict(int)

        for i in range(len(nums)):
            
            for j in range(i):

                graph[nums[i]*nums[j]] += 1
        
        return reduce(lambda a,b: ((b*(b-1))//2)*8 + a, graph.values(), 0)
    ```