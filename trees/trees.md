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
                # since left node 
                traverse.append(node.val)
                if node.right != None:
                    stack.append(node.right)
        
        return traverse

```