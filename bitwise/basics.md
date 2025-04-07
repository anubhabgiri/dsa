# Bit Operation Basics

### Count set bits in a number

```python
def  countSetBits(n):
    count = 0
    while (n):
        count += n & 1
        n >>= 1
    return count
```

``` python
# 1 - 0000000000000001 - 2 power 0 
# 2 - 0000000000000010 - 2 power 1
# 3 - 0000000000000011
# 4 - 0000000000000100 - 2 power 2
# 5 - 0000000000000101
# 6 - 0000000000000110
# 7 - 0000000000000111
# 8 - 0000000000001000 - 2 power 3

# corollary 1 - 2^m and 2^n will never have a common set bit because 1. 2^x will always have one set bit 2. since m and n are different, they will have different set bits

# corollary 2 - all numbers between 2^x (a) and 2^(x+1) (b) will have one common set bit with 2^x and no common bit set with 2^x+1 and could have a set bit with 2^x-1 or lower

# transitive corollary 3 - all numbers between 2^x (a) and 2^(x+1) (b)
```