# Basic boiler plates

### create adjacency list 

This is a very common code used in solving graph problems

```python

edges = [[1,2],[2,3],[3,4],[1,4],[1,5]]

adjacencyList = dict()

for edge in edges:
    if edge[0] in adjacencyList:
        adjacencyList[edge[0]].append(edge[1])
    else:
        adjacencyList[edge[0]] = [edge[1]]

print(adjacencyList)
```