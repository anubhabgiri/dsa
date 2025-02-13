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