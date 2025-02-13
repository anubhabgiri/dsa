# Matrix problems

### [999. Available Captures For Rook](https://leetcode.com/problems/available-captures-for-rook/description/?envType=problem-list-v2&envId=matrix)
```python
class Solution:
    def numRookCaptures(self, board: List[List[str]]) -> int:
        # it is guaranteed that there will 1 rook in the matrix

        # iterate through the matrix to find the position of rook
        row = None
        col = None
        for i in range(8):
            for j in range(8):
                if board[i][j] == 'R':
                    row, col = i, j
                    break
        
        ans = 0
        # There are 4 directions top, bottom, left, right
        # for each direction we will traverse outwards in the board
        # from the rook position
        # if a pawn is found, we can increment the attack count and stop traversing
        # if a bishop is found, we can stop traversing
        for i in reversed(range(row)):
            if board[i][col] == 'p':
                ans += 1
                break
            elif board[i][col] == 'B':
                break

        for i in range(row+1, 8):
            if board[i][col] == 'p':
                ans += 1
                break
            elif board[i][col] == 'B':
                break


        for i in reversed(range(col)):
            if board[row][i] == 'p':
                ans += 1
                break
            elif board[row][i] == 'B':
                break
        

        for i in range(col+1, 8):
            if board[row][i] == 'p':
                ans += 1
                break
            elif board[row][i] == 'B':
                break

        return ans
        
```

### [2500. Delete Greatest Value in Each Row](https://leetcode.com/problems/delete-greatest-value-in-each-row/description/?envType=problem-list-v2&envId=matrix)

```python
class Solution:
    def deleteGreatestValue(self, grid: List[List[int]]) -> int:

        # sort each row in the grid
        # if we do this, we can ensure that 
        # from right hand side, each column will have the greatest element in each row
        grid = [sorted(x) for x in grid]

        ans = 0
        # simply iterate through each column and add the greatest element across the rows to the answer
        # the direction of column iteration doesn't matter 
        for i in range(len(grid[0])):
            ans += max([grid[j][i] for j in range(len(grid))])

        return ans
```

### [566. Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/description/?envType=problem-list-v2&envId=matrix)

```python
class Solution:
    def matrixReshape(self, mat: List[List[int]], r: int, c: int) -> List[List[int]]:
        if r*c != len(mat)*len(mat[0]) or (r==len(mat) and c ==len(mat[0])):
            return mat
        
        li = []

        for row in mat:
            li.extend(row)
        
        it = iter(li)

        grid = []

        for i in range(r):
            row = []
            for j in range(c):
                row.append(next(it))
            grid.append(row)
        return grid
```