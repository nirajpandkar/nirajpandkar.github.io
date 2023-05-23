---
title: "#49 Group Anagrams"
date: 2023-05-22
draft: false

tags: ['hashmap']
categories: ['LeetCode']
toc: true
---

## Link
https://leetcode.com/problems/group-anagrams/description/

## Solution
1. Generating a custom key function is necessary. 
    - The custom key function in this case initializes a vector of 26 zeroes each represeting a letter in the alphabet.
    - Each zero will be incremented by 1 giving us the count of letters in the given word.
2. Time analysis:
    - All the strings in the input array are going to be tranversed once. `O(N)` where `N` is the total number of strings in the input array.
    - If the max length of a string in the input array is `k`, the total time complexity of the given problem solution is `O(Nk)`.
## Code
### C++
```C++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        map<vector<int>, vector<string>> anagram_list;
        for(auto &str: strs){
            anagram_list[getKey(str)].push_back(str);
        }

        vector<vector<string>> ans;
        for(auto &x: anagram_list){
            ans.push_back(x.second);
        }
        return ans;
    }

    vector<int> getKey(string str){
        vector<int> v(26, 0);

        for(auto &letter: str){
            v[letter - 'a'] += 1;
        }
        return v;
    }
};
```

## Notes
1. Make sure to add 1 for each occurrence of letter in the word.