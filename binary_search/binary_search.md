# Binary Search

## [2594. Minimum Time to Repair Cars](https://leetcode.com/problems/minimum-time-to-repair-cars/description/?envType=daily-question&envId=2025-03-16)

```python
class Solution:
    def isRepairPossible(self, time: int, cars: int, ranks: List[int]) -> bool:
        carCount = 0
        # calculate given time t how many cars in total can be repaired
        for rank in ranks:
            carCount += int(math.sqrt(time//rank))
            # interim check
            if carCount >= cars:
                return True
        # final check
        return carCount >= cars

    def repairCars(self, ranks: List[int], cars: int) -> int:

        # compute the max possible time required by any worker
        # this will define the upper boundary of binary search
        high = max(ranks)*cars*cars

        # type 2 binary search as we do not require an osscilatory search
        b = high//2
        while b >= 1:

            # at each step we check if the time is enough to repair all cars
            while (high - b) >= 1 and self.isRepairPossible(high - b, cars, ranks):
                # keep reducing until the boundary is reached
                high -= b

            b //= 2 
        
        return high
```