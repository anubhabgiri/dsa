# Depth First Search

### [2658. Maximum Number of Fish in a Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/description/)
```python
class Solution:
    def countFishes(self, i, j) -> int:
        if i >= self.m or i < 0 or j < 0 or j >= self.n:
            return 0
        
        if self.visited[i][j]:
            return 0

        self.visited[i][j] = True
        
        if self.grid[i][j] == 0:
            return 0

        return (self.grid[i][j] + self.countFishes(i+1, j) + self.countFishes(i-1, j) + self.countFishes(i, j+1) + self.countFishes( i, j-1))
        
    def findMaxFish(self, grid: List[List[int]]) -> int:
        self.m = len(grid)
        self.n = len(grid[0])
        self.grid =  grid

        self.visited = [[False] * self.n for _ in range(self.m)]

        result = 0

        for i in range(self.m):
            for j in range(self.n):
                if self.grid[i][j] > 0 and not self.visited[i][j]:
                    result = max(result, self.countFishes(i, j))
        
        return result
```