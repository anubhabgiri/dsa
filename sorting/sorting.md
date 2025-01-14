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