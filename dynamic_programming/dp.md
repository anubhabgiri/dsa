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