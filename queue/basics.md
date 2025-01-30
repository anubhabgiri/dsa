# Queue Basics

### Python performance metrics

using list vs dequeue as a queue

Code
```python
from collections import deque
import time

arr = ['a', 'b', 'c', 'd', 'e']

li = arr.copy()

stt = time.time()
print(f"starting list pop at index 0")
print(li.pop(0))
print(li.pop(0))
print(li.pop(0))
print(li.pop(0))
print(li.pop(0))
print(f"list pop completed {time.time() - stt}")

queue = deque(arr)

stt = time.time()
print(f"starting queue pop")
print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
print(queue.popleft())
print(f"queue pop completed {time.time() - stt}")
```

Output

```
starting list pop at index 0
a
b
c
d
e
list pop completed 0.0009183883666992188
starting queue pop
a
b
c
d
e
queue pop completed 0.0009751319885253906
```