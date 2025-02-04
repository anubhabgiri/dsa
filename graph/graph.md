# Graphs

### Course Schedule II
```python

from collections import defaultdict, deque

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> list:
        # Initialize graph and in-degree count
        graph = defaultdict(list)
        in_degree = [0] * numCourses
        
        # Build the graph and in-degree array
        for a, b in prerequisites:
            graph[b].append(a)
            in_degree[a] += 1
        
        # Find all nodes with zero in-degree
        zero_in_degree = deque([i for i in range(numCourses) if in_degree[i] == 0])
        
        # Perform topological sort
        order = []
        while zero_in_degree:
            course = zero_in_degree.popleft()
            order.append(course)
            for neighbor in graph[course]:
                in_degree[neighbor] -= 1
                if in_degree[neighbor] == 0:
                    zero_in_degree.append(neighbor)
        
        # Check if all courses are in the order
        return order if len(order) == numCourses else []

```

### [Number of Provinces](https://leetcode.com/problems/number-of-provinces/description/?envType=problem-list-v2&envId=graph)

This is one of the most common patterns in Graph problems. It begins with creating an adjancency list (if not provided directly) from the input.
The second step is to use DFS to traverse the graph. The idea is to traverse all the connected nodes. 

```python
class Solution:
    def solve(self, num) -> None:
        if self.visited[num] == 1:
            return False
        
        self.visited[num] = 1
        for t in self.mapper[num]:
            if self.visited[t] == 0:
                self.solve(t)
        return True


    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        self.mapper = dict()
        n = len(isConnected)

        # create adjacency list
        for i in range(n):
            for j in range(n):

                if isConnected[i][j] == 1:
                    if i in self.mapper:
                        self.mapper[i].append(j)
                    else:
                        self.mapper[i] = [j]
        
        self.visited = [0]*n
        self.numProvinces = 0

        for i in range(n):
            if self.solve(i):
                self.numProvinces += 1
        
        return self.numProvinces
```


### [2285. Maximum Total Importance of Roads](https://leetcode.com/problems/maximum-total-importance-of-roads/description/?envType=problem-list-v2&envId=graph)

```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        graph = defaultdict(list)
        for i, j in roads:
            graph[i].append(j)
            graph[j].append(i)
        
        weightList = sorted([(len(v), k) for k, v in graph.items()], reverse=True)

        assignedWeight = [0]*n

        k = n
        sum = 0
        for i, j in weightList:
            sum += i*k
            k -= 1

        return sum
```