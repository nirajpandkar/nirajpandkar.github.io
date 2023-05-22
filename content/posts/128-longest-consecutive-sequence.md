---
title: "#128 Longest Consecutive Sequence"
date: 2023-05-21
draft: false

tags: ['leetcode', 'union-find']
categories: ['LeetCode']
toc: true
---
### Todo: 
1. Explanation of solution
    - Time complexity
2. What patterns were applied - 
    - complement of target (two-sum problem technique)
    - union find (for connected component)

## Link
https://leetcode.com/problems/longest-consecutive-sequence/description/

## Solution

## Code
### Python
```python
class UnionFind:
    def __init__(self, n_size):
        self.root = [i for i in range(n_size)]
        self.size = [1 for i in range(n_size)]
        self.max_size = 1
    def find(self, x):
        while x != self.root[x]:
            x = self.root[x]
        return x
    def union(self, x, y):
        rootX = self.find(x)
        rootY = self.find(y)
        if rootX != rootY:
            self.root[rootY] = rootX
            self.size[rootX] += self.size[rootY]
            if self.size[rootX] > self.max_size:
                self.max_size = self.size[rootX]
    def get_longest_sequence_size(self):
        return self.max_size



class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if len(nums) < 2:
            return len(nums)

        nums = list(set(nums))
        uf = UnionFind(len(nums))
        
        num_dict = dict()
        for i in range(len(nums)):
            if (nums[i] + 1) in num_dict:
                uf.union(num_dict[nums[i] + 1], i)
            if (nums[i] - 1) in num_dict:
                uf.union(num_dict[nums[i] - 1], i)
            num_dict[nums[i]] = i

        return uf.get_longest_sequence_size()
```

## Notes
1. Make sure to add the size of the root node for which the root is being changed.