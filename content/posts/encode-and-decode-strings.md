---
title: "#271 Encode and Decode Strings"
date: 2023-05-24
draft: false

tags: ['string manipulation', 'python']
categories: ['LeetCode']
toc: true
---

## Link
https://leetcode.com/problems/encode-and-decode-strings/description/

## Solution
1. I just used all the punctuations given by `string.punctuation` in python as the delimiter. Obvious flaw here; if the same kind of string exists in the actual string, it is going to read it as a delimiter. (It was one of those days. Tired + no motivation; but can't miss two days in a row hehe)
2. To combat that, there's an approach which is agnostic to the type of delimeter [Reference](https://leetcode.com/problems/encode-and-decode-strings/solutions/70443/accepted-simple-c-solution/)
    1. rather it sequentially looks for a `number` followed by a special character (@).
    2. For the next `number` of letters, it reads the string and appends it to the list. 
    3. Repeat the above steps till you reach the end of the string.

## Code
### Python
```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        all_puncts = string.punctuation
        return all_puncts.join(strs)

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        return s.split(string.punctuation)
```

## Notes
1. The one and only Stefan Pochmann has commented on the reference user solution. Pretty handy tip :)