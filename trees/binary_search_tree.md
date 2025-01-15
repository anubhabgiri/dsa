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

## [654. Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/description/)

```python
class Solution:

    def maxIndex(self, start: int, stop: int) -> int:

        maxNumIndex = start

        for i in range(start, stop):

            if self.nums[i] > self.nums[maxNumIndex]:
                
                maxNumIndex = i

        return maxNumIndex

    def construct(self, start: int, stop: int) -> Optional[TreeNode]:

        if start == stop:

            return None

        maxNumIndex = self.maxIndex(start, stop)

        node = TreeNode(self.nums[maxNumIndex])

        node.left = self.construct(start, maxNumIndex)

        node.right = self.construct(maxNumIndex+1, stop)

        return node


    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:

        self.nums = nums
        
        root = self.construct(0, len(nums))

        return root
```