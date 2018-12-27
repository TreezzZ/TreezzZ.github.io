---
layout: post                                                    
title:  "UOJ_2 the kth number"
categories: 算法
tags: 算法 分治
author: Tree
---

* content                                                       
{:toc}

# Problem description
Find the kth largest element in an unsorted array A . Note that it is the kth largest element in the sorted order, not the kth distinct element. The range of length of A is N(1≤N≤5,000,000) and the element (integer) in A is no bigger than 10,000,00000.

# Input
Line 1: the length of the unsorted array A and the index k. Line 2: the all elements in array A and split by spaces

# Output
Line 1: A single integer that is the kth largest element in an unsorted array A.

# Sample Input 1
```
8 2
1 3 5 7 4 2 6 8
```

# Sample Output 1
```
7
```

# Sample Input 2
```
8 2
1 1 2 2 3 3 4 4
```

# Sample Output 2
```
4
```

---

# 思路
有一个很直观的思路：排序，返回第k个数。时间复杂度为O(nlogn)。下面介绍采用划分思想，使时间复杂度达到O(n)。<br />
1. 和快排中划分的思想一样，将数组划分为左右两部分，返回pivot。
2. 如果k == pivot，也就是说正好这个位置就是第k个元素。为什么呢？划分的性质就是每一趟将一个元素安排到最终的排序的位置。在pivot左边的元素都大于（小于）pivot，在pivot右边的元素都小于（大于）pivot。但左右子数组本身并不一定是有序的。
3. 如果k < pivot，说明第k个元素还在左边的数组里，需要继续递归查找左半部分。
4. 如果k > pivot，说明第k个元素还在右边的数组里，需要继续递归查找右半部分。

# 代码
```
# -*- coding:utf-8 -*-

"""UOJ第二题，the kth number。最后两个数据点超内存过不了，无解，OJ有问题。
"""

import random


def select_kth_largest(arr, left, right, k):
    """选择数组中第k大数

    Args:
        arr(list): 数组
        left(int): 数组中第一个元素下标
        right(int): 数组中最后一个元素下标
        k(int): 选择第k大数

    Returns:
        ans(int): 第k大数
    """
    pivot = random_partition(arr, left, right)
    n = pivot - left + 1
    if n == k:
        return arr[pivot]
    elif k < n:
        return select_kth_largest(arr, left, pivot-1, k)
    else:
        return select_kth_largest(arr, pivot+1, right, k-n)


def random_partition(arr, left, right):
    """随机选择一个数作为pivot

    Args:
        arr(list): 数组
        left(int): 数组第一个元素下标
        right(int): 数组中最后一个元素下标

    Returns:
        pivot(int): pivot
    """
    pivot = random.randint(left, right)
    arr[left], arr[pivot] = arr[pivot], arr[left]
    return partition(arr, left, right)


def partition(arr, left, right):
    """产生划分

    Args:
        arr(list): 数组
        left(int): 数组第一个元素下标
        right(int): 数组最后一个元素下标

    Returns:
        pivot(int): pivot
    """
    i, j = left, right
    tmp = arr[left]
    while i < j:
        while i < j and arr[j] <= tmp:
            j -= 1
        if i < j:
            arr[i] = arr[j]
        while i < j and arr[i] >= tmp:
            i += 1
        if i < j:
            arr[j] = arr[i]
    arr[i] = tmp

    return i


if __name__ == '__main__':
    n, k = list(map(int, input().split()))
    arr = list(map(int, input().split()))
    print(select_kth_largest(arr, 0, len(arr)-1, k))

```