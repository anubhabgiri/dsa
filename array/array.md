# Array

### [1726. Tuple with Same Product](https://leetcode.com/problems/tuple-with-same-product/description/)

```python
class Solution:
    def tupleSameProduct(self, nums: List[int]) -> int:
        graph = defaultdict(int)

        for i in range(len(nums)):
            
            for j in range(i):

                graph[nums[i]*nums[j]] += 1
        
        return reduce(lambda a,b: ((b*(b-1))//2)*8 + a, graph.values(), 0)
```


### [3160. Find the number of distinct colors among the balls](https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls/description/)

```python
class Solution:
    def queryResults(self, limit: int, queries: List[List[int]]) -> List[int]:
        
        
        balls = defaultdict(int) # balls will contain the latest color 
        colors = defaultdict(int) # colors will contain the count 
        ans = []

        for i, j in queries:
            # if ball is already mapped
            if i in balls:
                color = balls[i]
                # update the new color
                balls[i] = j
                # readjust colors graph
                if color in colors:
                    if colors[color] > 1:
                        colors[color] -= 1
                    else:
                        colors.pop(color)
                # add the new color
                colors[j] += 1
            
            else:
                # add color to the ball
                balls[i] = j
                # update the colors graph
                colors[j] += 1
            ans.append(len(colors.keys()))
        return ans
```


### [1352. Product of the Last K Numbers](https://leetcode.com/problems/product-of-the-last-k-numbers/)

This follows the approach of prefix sum but also takes into consideration when 0 appears

```python
class ProductOfNumbers:

    def __init__(self):
        self.products = [1]

    def add(self, num: int) -> None:

        if num == 0:
            self.products = [1]
        else:
            self.products.append(num*self.products[-1])

    def getProduct(self, k: int) -> int:
        if k >= len(self.products):
            return 0
        else:
            return self.products[-1]//self.products[len(self.products)-k-1]
```

### [228. Summary Ranges](https://leetcode.com/problems/summary-ranges/?envType=problem-list-v2&envId=array)

```python

class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        if len(nums) == 0:
            return []
        ans = []
        start = nums[0]
        end = None
        for i in range(1, len(nums)):
            if nums[i] != nums[i-1] + 1:

                if end != None and end != start:
                    s = f"{start}->{end}"
                else:
                    s = str(start)
                ans.append(s)
                start = nums[i]
                end = None
            else:
                end = nums[i]

        if end != None and end != start:
            s = f"{start}->{end}"
        else:
            s = str(start)
        ans.append(s)
        return ans
```

### [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/?envType=problem-list-v2&envId=array)

This solution doesn't use any extra space and runs in linear time complexity

The idea is to traverse the array and for each number mark the corresponding correct position of the array as negative of the existing value in that position

For e.g., if the input is nums = [4,3,2,7,8,2,3,1]

in iteration 1, the number is 4 and the correct position is 3 (0 indexed), so we modify the array in-place to [4,3,2,-7,8,2,3,1]

in iteration 2, the number is 3 and the correct position is 2, so we modify the array to [4,3,-2,-7,8,2,3,1]

- Q. Why are we not simply modifying the value to -1 which would mark that position as well?

- A. If we do that, we are also ignoring the value that was originally there in that position.

- Q. Why are we adding an if condition before marking the correct index?

- A. Since there are missing values in the array but the size of array is n, it means that some numbers appears more than once and so, if we flip the same position twice or even number of times without checking, it will end up as a positive number leading to error in the final ans. 

Since 
```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:

        for i in range(len(nums)):

            index = abs(nums[i]) - 1

            if nums[index] > 0:
                nums[index] = -nums[index]

        
        return [ i+1 for i, val in enumerate(nums) if val > 0]
```

### [561. Array Partition](https://leetcode.com/problems/array-partition/?envType=problem-list-v2&envId=array)

```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        # to maximize, we need to put numbers with minimum difference together
        # to achieve that, we need to sort the array
        nums.sort()
        i = 1
        maxSum = 0
        # now we only need to add the min of every pair of numbers starting from the beginning
        while i < len(nums):
            maxSum += min(nums[i], nums[i-1])
            i += 2
        
        return maxSum
```

### [575. Distribute Candies](https://leetcode.com/problems/distribute-candies/?envType=problem-list-v2&envId=array)

```python
class Solution:
    def distributeCandies(self, candyType: List[int]) -> int:
        # there are 2 possibilities
        # 1. The number of unique candy types is greater than n/2 in which case Alice is free to choose from multiple options
        # 2. The number of unique candy types is less than n/2, so the maximum count of unique candies she can eat is the count of unique candies available
        n = len(candyType)
        candyType = set(candyType)

        return min(n//2, len(candyType))
```