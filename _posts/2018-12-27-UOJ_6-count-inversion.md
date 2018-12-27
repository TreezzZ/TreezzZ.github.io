---
layout: post                                                    
title:  "UOJ_6 Count Inversion"
categories: 算法
tags: 算法 分治
author: Tree
---

* content                                                       
{:toc}

# Problem Description
Recall the problem of finding the number of inversions. As in the course, we are given a sequence of n numbers a1,a2,⋯,an, and we define an inversion to be a pair i < j such that ai > aj.

We motivated the problem of counting inversions as a good measure of how different two orderings are. However, one might feel that this measure is too sensitive. Let's call a pair a significant inversion if i<jand ai>3aj. Give an O(nlogn) algorithm to count the number of significant inversions between two orderings.

The array contains N elements (1<=N<=100,000). All elements are in the range from 1 to 1,000,000,000.

# Input
The first line contains one integer N, indicating the size of the array. The second line contains N elements in the array. <br />

* 50% test cases guarantee that N < 1000.

# Output
Output a single integer which is the number of pairs of significant inversions.

# Sample Input
```
6
13 8 5 3 2 1
```

# Sample Output
```
6
```

---

# 思路
分治解法，逆序数对为左半部分逆序数+右半部分逆序数+跨越左右部分逆序数，其中重点在求跨越左右部分逆序数。我们可以对左右部分分别排序，然后在O(n)的时间内求出跨越左右部分逆序数。具体的，对于右边数组的每一个元素，如果对左边数组的一个元素出现了a[i] > 3a[j]，那么i后的所有元素，都满足这个条件，可以直接计算得到结果。还有一个trick是，可以在求跨越左右逆序数时进行归并排序，这样就进一步降低了时间复杂度。

# 代码
```
# -*- coding:utf-8 -*-

"""UOJ第6题。
"""

import copy


def count_inversion(arr, aux, left, right):
    """逆序数对，a_i>3a_j

    Args:
        arr(list): 数组
        aux(list): 辅助空间
        left(int): 数组第一个元素下标
        right(int): 数组最后一个元素下标

    Returns:
        inversion_num(int): 逆序数
    """
    if left == right:
        return 0
    elif right - left == 0 and arr[left] > 3 * arr[right]:
        return 1

    mid = left + (right - left) // 2
    left_inversion_num = count_inversion(arr, aux, left, mid)
    right_inversion_num = count_inversion(arr, aux, mid+1, right)
    cross_inversion_num = count_merge(arr, aux, left, mid, right)

    return left_inversion_num + right_inversion_num + cross_inversion_num


def count_merge(arr, aux, left, mid, right):
    """计算两个数组逆序数并且归并排序

    Args:
        arr(list): 数组
        left(int): 左半数组第一个元素下标
        mid(int): 左半数组最后一个元素下标
        right(int): 右半数组最后一个元素下标
    """
    cross_inversion_count = 0
    i, j = left, mid+1
    while i <= mid and j <= right:
        if arr[i] > 3 * arr[j]:
            # 后面的都会满足条件，直接计算即可
            cross_inversion_count += mid - i + 1
            j += 1
        else:
            i += 1

    for i in range(left, right+1):
        aux[i] = arr[i]

    # 归并排序
    i, j, k = left, mid+1, left
    while k <= right:
        if i <= mid and j <= right:
            if aux[i] < aux[j]:
                arr[k] = aux[i]
                i += 1
            else:
                arr[k] = aux[j]
                j += 1
        elif i <= mid:
            arr[k] = aux[i]
            i += 1
        else:
            arr[k] = aux[j]
            j += 1
        k += 1

    return cross_inversion_count


if __name__ == '__main__':
    N = int(input())
    arr = list(map(int, input().split()))
    aux = copy.deepcopy(arr)
    print(count_inversion(arr, aux, 0, len(arr)-1))

```