# Prefix Sum

### [Grid Game](https://leetcode.com/problems/grid-game/description/)

```python
class Solution:
    def gridGame(self, grid: List[List[int]]) -> int:
        
        n = len(grid[0])

        # calculate prefix sum of each row
        gridSum = [[], []]

        t1 = 0
        t2 = 0

        for i in range(n):

            t1 += grid[0][i]
            t2 += grid[1][i]

            gridSum[0].append(t1)
            gridSum[1].append(t2)

        # capture the maximum that can be captured by robot 2 
        # considering this is the inflection point for robot 1
        maxM = []

        for i in range(n):

            maxM.append(max(gridSum[0][n-1] - gridSum[0][i], gridSum[1][i-1] if i > 0 else 0))

        return min(maxM)

        
```