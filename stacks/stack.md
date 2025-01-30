# Stack

[Leetcode list](https://leetcode.com/problem-list/stack/)

## Basic Stack Pattern

The following problems can be solved using the same pattern 

- Remove Outermost Parentheses
- Make the String Great
- Baseball Game
- Crawler Log Folder

### pseudo code

```
stack = []

for element in elements

    if condition stack.pop()
    else stack.push(element)

return stack
```

### [1441. Build an Array With Stack Operations](https://leetcode.com/problems/build-an-array-with-stack-operations/description/?envType=problem-list-v2&envId=stack)

```python
class Solution:
    def buildArray(self, target: List[int], n: int) -> List[str]:
        stack = []
        j = 0
        for i in range(1, n+1):
            if i == target[j]:
                stack.append("Push")
                j += 1
            else:
                stack.extend(["Push", "Pop"])

            if j >= len(target):
                break

        return stack
```

### [1700. Number of Students Unable to Eat Lunch](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/description/?envType=problem-list-v2&envId=stack)

Intuition: This problem cannot be solved by simply computing the total number of mismatches as the order in which the sandwich appears is important

```python
from collections import deque
class Solution:
    def countStudents(self, students: List[int], sandwiches: List[int]) -> int:
        sandwichStack = list(reversed(sandwiches))
        studentQueue = deque(students)

        lastServed = 0

        while len(studentQueue) > 0 and lastServed < len(studentQueue):

            if sandwichStack[-1] == studentQueue[0]:
                sandwichStack.pop(-1)
                studentQueue.popleft()
                lastServed = 0
            else:
                studentQueue.append(studentQueue.popleft())
                lastServed += 1

        return len(studentQueue)
```

### [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/?envType=problem-list-v2&envId=stack)

```python
from collections import Counter
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        mapper = {value: index for index, value in enumerate(nums1)}
        ans = [-1]*(len(nums1))

        stack = []
        sol = [-1]*(len(nums2))

        for i in reversed(range(len(nums2))):

            while len(stack) > 0 and stack[-1] < nums2[i]:
                stack.pop()
            
            if len(stack) > 0:
                sol[i] = stack[-1]

            stack.append(nums2[i])
            if nums2[i] in mapper:
                ans[mapper[nums2[i]]] = sol[i]


        return ans
```
