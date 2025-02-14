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


### [3160. Find the number of distinct colors among the balls](https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls/description/)

```python
class Solution:
    def queryResults(self, limit: int, queries: List[List[int]]) -> List[int]:
        
        
        balls = defaultdict(int) # balls will contain the latest color 
        colors = defaultdict(int) # colors will contain the count 
        ans = []

        for i, j in queries:
            # if ball is already mapped
            if i in balls:
                color = balls[i]
                # update the new color
                balls[i] = j
                # readjust colors graph
                if color in colors:
                    if colors[color] > 1:
                        colors[color] -= 1
                    else:
                        colors.pop(color)
                # add the new color
                colors[j] += 1
            
            else:
                # add color to the ball
                balls[i] = j
                # update the colors graph
                colors[j] += 1
            ans.append(len(colors.keys()))
        return ans
```


### [1352. Product of the Last K Numbers](https://leetcode.com/problems/product-of-the-last-k-numbers/)

This follows the approach of prefix sum but also takes into consideration when 0 appears

```python
class ProductOfNumbers:

    def __init__(self):
        self.products = [1]

    def add(self, num: int) -> None:

        if num == 0:
            self.products = [1]
        else:
            self.products.append(num*self.products[-1])

    def getProduct(self, k: int) -> int:
        if k >= len(self.products):
            return 0
        else:
            return self.products[-1]//self.products[len(self.products)-k-1]
```

### [228. Summary Ranges](https://leetcode.com/problems/summary-ranges/?envType=problem-list-v2&envId=array)

```python

class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        if len(nums) == 0:
            return []
        ans = []
        start = nums[0]
        end = None
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1] + 1:

                if end != None and end != start:
                    s = f"{start}->{end}"
                else:
                    s = str(start)
                ans.append(s)
                start = nums[i]
                end = None
            else:
                end = nums[i]

        if end != None and end != start:
            s = f"{start}->{end}"
        else:
            s = str(start)
        ans.append(s)
        return ans
```