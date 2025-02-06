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