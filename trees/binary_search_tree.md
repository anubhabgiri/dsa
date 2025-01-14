# Binary Search Tree

## [501. Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/description/?envType=problem-list-v2&envId=tree)

```python
class Solution:
    def helper(self, node: Optional[TreeNode]) -> None:
        if node == None:
            return

        if node.val in self.mapp:
            self.mapp[node.val] += 1
        else:
            self.mapp[node.val] = 1
        
        self.helper(node.left)
        self.helper(node.right)
        
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        self.mapp = dict()
        self.helper(root)
        maxCount = max(self.mapp.values())

        return [ x for x in self.mapp.keys() if self.mapp[x] == maxCount]

```

## [589. N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal/description/?envType=problem-list-v2&envId=tree)

```python

class Solution:
        
    def preorder(self, root: 'Node') -> List[int]:
        
        traverse = []
        
        stack = [root]

        while len(stack) > 0:

            node = stack.pop(-1)

            if node == None:
                
                continue

            traverse.append(node.val)

            for child in node.children[::-1]:

                stack.append(child)
            
        return traverse

```