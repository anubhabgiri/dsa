# Sorting

### Selection Sort

```cpp
     	for(int i=0; i<n; i++){
     		min_index = arr[i];
     		for(int j=i+1; j<n; j++){
     			if arr[min_index] > arr[j]
     		min_index = j;}
     		if(min_index != i)
     	swap(arr[i], arr[min_index]);}
```


### [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

```python
class Solution:
    def findMedianSortedArrays(self, ar1: List[int], ar2: List[int]) -> float:
        arr = []

        i = 0
        j = 0

        while i < len(ar1) and j < len(ar2):

            if ar1[i] < ar2[j]:
                arr.append(ar1[i])
                i += 1
            
            else:
                arr.append(ar2[j])
                j += 1


        while i < len(ar1):

            arr.append(ar1[i])
            i += 1

        while j < len(ar2):

            arr.append(ar2[j])
            j += 1
        
        print(arr)
        n = len(arr)
        if n%2 == 0:
            
            return (arr[n//2] + arr[n//2 -1])/2
        
        else:
            return float(arr[n//2])
```