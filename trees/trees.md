# Trees

All code related to binary and n-ary trees

## In order traversal

order of traversal `left --> root --> right`

``` python 
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        # start with the root node
        stack = [root]
        traverse = []
        
        # iterate till there is no 
        while len(stack) > 0:
            node = stack.pop(-1)

            # 
            if node == None:
                continue

            if node.left != None:
                # copying left node to another node
                left = node.left
                # adding the current node back to the stack as the value needs to be added to traverse
                stack.append(node)
                # adding the copied left node to the stack since it needs to be processed first
                stack.append(left)
                # making the left pointer NULL to avoid infinite loop
                node.left = None
                
            else:
                # since left node is processed or not present, the root node can be processed
                traverse.append(node.val)
                # only right node remains, so it is added to the stack
                if node.right != None:
                    stack.append(node.right)
        
        return traverse

```

## [Find Largest Value in Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/?envType=problem-list-v2&envId=tree)

Using recursive function

```python

class Solution:
    def helper(self, node: Optional[TreeNode], level: int) -> None:

        if node == None:
            
            return
        
        if level not in self.levelMap:

            self.levelMap[level] = node.val

        else:

            self.levelMap[level] = max(node.val, self.levelMap[level])
        
        self.helper(node.left, level+1)
        self.helper(node.right, level+1)
            
        
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        
        self.levelMap = dict()
        
        self.helper(root, 0)

        return [x for x in self.levelMap.values()]

```

Using iterative method 

```python
class Solution:
        
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        
        levelMap = dict()

        
        stack = [(root, 0)]
        
        while len(stack) > 0:

            node, level = stack.pop(-1)
            
            if node == None:
                
                continue

            if level not in levelMap:

                levelMap[level] = node.val
            
            else:

                levelMap[level] = max(levelMap[level], node.val)

            
            stack.append((node.left, level+1))

            stack.append((node.right, level+1))
        

        return [x for x in levelMap.values()]
```