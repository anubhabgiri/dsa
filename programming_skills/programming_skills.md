### [Find The Difference](https://leetcode.com/problems/find-the-difference/?envType=study-plan-v2&envId=programming-skills)

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        # sort both the strings
        s = "".join(sorted(s))
        t = "".join(sorted(t))
        # whatever doesn't match must be the misfit
        for i in range(len(s)):
            if s[i] != t[i]:
                return t[i]

        return t[-1]

# a better way to do this is to count the alphabets in each string and delete the common ones
```

### [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description/?envType=study-plan-v2&envId=programming-skills)

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        found_index = -1
        if len(haystack) < len(needle):
            return -1
        for i in range(len(haystack)-len(needle)+1):
            if haystack[i] == needle[0]:
                k = i
                found_index = i
                for j in range(len(needle)):
                    if needle[j] != haystack[k]:
                        found_index = -1
                        break
                    k += 1
            if found_index != -1:
                return found_index
            
        return found_index
```

### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/?envType=study-plan-v2&envId=programming-skills)

```python
from collections import defaultdict
import string
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        sCount = defaultdict(int)
        tCount = defaultdict(int)

        # count the occurrences in each string
        for char in s:
            sCount[char] += 1
        for char in t:
            tCount[char] += 1

        # if there is a mismatch return False
        for letter in string.ascii_lowercase:
            if sCount[letter] != tCount[letter]:
                return False
        # otherwise it must be True
        return True
```

### [1041. Robot Bounded In Circle](https://leetcode.com/problems/robot-bounded-in-circle/description/?envType=study-plan-v2&envId=programming-skills)

```python
class Solution:
    def nextDirection(self, direction: str, instruction: str) -> str:
        pos = self.arr.index(direction)

        if instruction == 'L':
            return self.arr[abs((pos+4-1)%4)]
        else:
            return self.arr[(pos+1)%4]
        
    
    def isRobotBounded(self, instructions: str) -> bool:
        abcissa = 0
        ordinate = 0
        direction = "N"
        self.arr = ['N', 'E', 'S', 'W']
        for instruction in instructions:
            if instruction == 'G':
                if direction == 'N':
                    ordinate += 1
                elif direction == 'S':
                    ordinate -= 1
                elif direction == 'W':
                    abcissa -= 1
                else:
                    abcissa += 1
            else:
                direction = self.nextDirection(direction, instruction)
        # if at the end of the cycle the robot is back to origin, it will be true after n number of cycles
        if (abcissa == 0 and ordinate == 0):
            return True
        # else if the position is not origin but the direction of the robot is anything other than North
        # over multiple cycles the robot will go round in circles
        if direction != 'N':
            return True
        # else there is no way the robot will be contained in circles
        return False

```

### [54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/?envType=study-plan-v2&envId=programming-skills)

```python
class Solution:
    def findNextDirection(self, orientation: str, direction: str, pos: List[int]) -> List | None:
        # since the movement has to be spiral, the next direction is pretty determined
        # we have to check if that direction is legal or not
        # direction = self.directionMap(direction)
        # orientation = self.orientationMap(orientation)

        if direction == "left":
            if pos[1]-1 >= 0 and self.matrix[pos[0]][pos[1]-1] != -500:
                return [pos[0],pos[1]-1]
        elif direction == "right":
            if pos[1]+1 < self.n and self.matrix[pos[0]][pos[1]+1] != -500:
                return  [pos[0],pos[1]+1]
        elif direction == 'up':
            if pos[0]-1 >= 0 and self.matrix[pos[0]-1][pos[1]] != -500:
                return [pos[0]-1,pos[1]]
        elif direction == 'down':
            if pos[0]+1 < self.m and self.matrix[pos[0]+1][pos[1]] != -500:
                return [pos[0]+1,pos[1]]
        return None
                 


    def traverse(self, pos: List[int], orientation: str, direction: str) -> List:
        a, b = pos[0], pos[1]
        if direction == "up" and orientation == "col":
            while True:
                self.positions.append(self.matrix[a][b])
                self.matrix[a][b] = -500
                if a-1 >= 0 and self.matrix[a-1][b] != -500:
                    a -=1
                else: 
                    break
            return [a, b]
        elif direction == "down" and orientation == "col":
            while True:
                self.positions.append(self.matrix[a][b])
                self.matrix[a][b] = -500
                if a+1 < self.m and self.matrix[a+1][b] != -500:
                    a += 1
                else:
                    break
        elif direction == "right" and orientation == "row":
            while True:
                self.positions.append(self.matrix[a][b])
                self.matrix[a][b] = -500
                if b+1 < self.n and self.matrix[a][b+1] != -500:
                    b += 1
                else: 
                    break
        elif direction == "left" and orientation == "row":
            while True:
                self.positions.append(self.matrix[a][b])
                self.matrix[a][b] = -500
                if b-1 >= 0 and self.matrix[a][b-1] != -500:
                    b -=1
                else:
                    break
        return [a, b]

        
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        self.m = len(matrix)
        self.n = len(matrix[0])
        self.matrix = matrix
        self.positions  = []
        self.directionMap = {
            "up": "right",
            "down": "left",
            "right": "down",
            "left": "up"
        }

        self.orientationMap = {
            "row": "col",
            "col": "row"
        }

        pos = [0, 0]
        direction = "right"
        orientation = "row"
        while True:
            pos = self.traverse(pos, orientation, direction)
            # print(self.positions)
            orientation = self.orientationMap[orientation]
            direction = self.directionMap[direction]
            # print(orientation, direction)
            pos = self.findNextDirection(orientation, direction, pos)
            # print(pos)
            if pos is None:
                break

        return self.positions

# Note: this can be simplified a lot

```

### [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/description/?envType=study-plan-v2&envId=programming-skills)

```python

class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """

        m = len(matrix)
        n = len(matrix[0])

        rowSpace = [1 for i in range(m)]
        colSpace = [1 for i in range(n)]

        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    rowSpace[i] = 0
                    colSpace[j] = 0
        
        for i in range(m):
            for j in range(n):
                if rowSpace[i] == 0 or colSpace[j] == 0:
                    matrix[i][j] = 0
        # Note: This solution operates in O(m+n) space 
        # I want to solve this in O(1) space
```