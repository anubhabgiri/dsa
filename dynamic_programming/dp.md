# Dynamic Programming

### Longest Increasing Subsequence

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        maxLength = 0
        maxLengthArray = [1]*n

        for i in range(n):
            for j in range(i):
                if nums[j] < nums[i]:
                    maxLengthArray[i] = max(maxLengthArray[i], maxLengthArray[j] + 1)
            
            maxLength = max(maxLength, maxLengthArray[i])

        return maxLength
```

### Coins Change

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [0]*(amount+1)

        for i in range(1, amount+1):
            dp[i] = 10001
            
            for j in coins:

                if (i-j) >= 0:
                    
                    dp[i] = min(dp[i], (dp[i-j] + 1))

        if dp[amount] == 1e4+1:
            
            return -1
        
        return dp[amount]
```

### Coins Change II

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        
        dp = [0]*(amount+1)
        
        dp[0] = 1
        
        for coin in coins:
            for i in range(1, amount+1):

                if (i-coin) >= 0:
                    
                    dp[i] += dp[i-coin]
                
        return dp[amount]
```    

### Maximum Length of Pair Chain

Note: the algorithm is similar to longest increasing subsequence

```python 
class Solution:
    
    def findLongestChain(self, pairs: List[List[int]]) -> int:

        pairs.sort()
        
        longest = 0

        dp = [1]*(len(pairs))

        for i in range(len(pairs)):

            for j in range(i):

                if pairs[j][1] < pairs[i][0]:

                    dp[i] = max(dp[i], dp[j]+1 )
            
            longest = max(longest, dp[i])
        
        return longest
        
```

### [309. Best Time to Buy and Sell Stock with Cooldown](Best Time to Buy and Sell Stock with Cooldown)

```python
class Solution:
    
    def maxProfit(self, prices: List[int]) -> int:
        n = len(prices)

        dp = [0]*n

        for i in range(n):
            if i == 0:
                dp[i] = 0
            
            elif i == 1:
                
                dp[i] = max(0, prices[1]-prices[0])
            else:
                
                dp[i] = dp[i-1]
                
                for j in range(i):
                        prev = dp[j-2] if (j-2>=0) else 0
                        dp[i] = max(dp[i], prev + prices[i] - prices[j])

        return dp[n-1]
```

### [983. Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/description/?envType=problem-list-v2&envId=50vlu3z5)

```python
class Solution:
    def mincostTickets(self, days: List[int], costs: List[int]) -> int:
        
        lastDay = days[-1]

        dp = [0]*(lastDay + 1)

        i = 0

        for d in range(1, lastDay+1):

            if d < days[i]:

                dp[d] = dp[d-1]
            
            else:

                i += 1
                dp[d] = min(dp[d-1] + costs[0], dp[max(0, d-7)] + costs[1], dp[max(0, d-30)] + costs[2])
        

        return dp[lastDay]
```

### [279. Perfect Squares](https://leetcode.com/problems/perfect-squares/description/?envType=problem-list-v2&envId=50vlu3z5)
```python
import sys

class Solution:
    def is_perfect_square(self, n):
        i = 1
        while i*i <= n:
            if i*i == n:
                return True
            i += 1
        return False
    
    def numSquares(self, n: int) -> int:
        i = 1
        squares = []

        while i*i <= n:
            squares.append(i*i)
            i += 1

        dp = [0]*(n+1)

        for i in range(1, n+1):

            if self.is_perfect_square(i):

                dp[i] = 1
            
            else:

                dp[i] = sys.maxsize

                for square in squares:

                    if (i-square) >= 0:
                        
                        dp[i] = min(dp[i], dp[i-square] + 1)

        return dp[n]
```

### [416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/description/?envType=problem-list-v2&envId=50vlu3z5)

It cannot be done by computing the sum and checking if it is odd or even. It can be solved using a 0/1 knapsack approach.

```python
class Solution:
    
    def canPartition(self, nums: List[int]) -> bool:
        
        # compute the total sum of the elements
        sum = reduce(lambda a,b: a+b, nums)

        # boundary case: if the total sum is not even, it is guaranteed that equal subset 
        # cannot be achieved 
        if sum%2 != 0:
            
            return False

        target = sum//2
        
        n = len(nums)

        # create the memoization array 
        tab = [[0]*(target + 1) for y in range(n + 1)]

        # iterate each element
        # this is the outer loop since we do not want to count the same element twice
        for i in range(1, n+1):
            # for each element iterate through target weights from 1 to actual target
            for w in range(1, target+1):
                
                if nums[i-1] <= w:
                    # if element is less or equal to the current target
                    # we consider if it makes sense to include the element or not
                    # and take the max of it
                    include_item = nums[i-1] + tab[i-1][w-nums[i-1]]
                    exclude_item = tab[i-1][w]
                    tab[i][w] = max(include_item, exclude_item)
                else:
                    # if the element is greater then there is no computation
                    # it is simply the same as excluding the item in the previous step
                    # this step is important otherwise, it will continue to store the initialization val
                    tab[i][w] = tab[i-1][w]
        # the requirement is fulfilled only if the max sum achievable with given elements 
        # is equal to target sum
        return tab[n][target] == target
```

