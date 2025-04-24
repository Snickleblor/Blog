---
layout: post
title: Linear og binary search 
date: 2023-08-26
author: Simon
categories: programmering python
---

```python
import time

arr = [1, 54, 23, 512, 49, 382, 42, 0, 24]
arr = sorted(arr)
target = 42

"""
Example of linear search
"""
def linear_search():
    for i, n in enumerate(arr):
        if target == n: return True
"""
Example of binary search
"""
def binary_search():
    low = 0 
    high = len(arr) - 1 
    while low <= high:
        mid = (low + high)//2 
        if arr[mid] == target:
            return True
        elif arr[mid] > target:
            high = mid - 1
        elif arr[mid] < target:
            low = mid + 1

start_time = time.time()
linear_search()
print("--- %s seconds ---" % (time.time() - start_time))

start_time = time.time()
binary_search()
print("--- %s seconds ---" % (time.time() - start_time))
```
