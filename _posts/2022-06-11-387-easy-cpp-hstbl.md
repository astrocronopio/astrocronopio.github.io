---
layout: post
title: (c++) 387 - First Unique Character in a String
categories: [Leetcode, cpp]
---


Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.


### Brute force

##### Input: s = "leetcode"

- I take a look at l, I check if does repeat I go next. In this case it doesnt so it is the solution. We only care about the first one which doesnt repeat.

##### Input: s = "aaccaddleetcode"

- I take a look at a, I check if does repeat I go next. In this case it repeat thefore I skip. Next value is also a, as before, so we should delete all the instances of a to be sure.

- Now the input is s = "ccddleetcode", we repeat the previous step
- Now the input is s = "ddleetcode", we repeat the previous step
- Now the input is s = "leetcode", we repeat the previous step
- Now L doesnt repeat so it is the solution, its position in the original input was 4.


This is a $O(n^2)$


### Bottlenecks

Searching the repeated values makes the solution slow. Ideally we could make something like this

x = (frecuency, first index)	
"a = (3,0)
 c = (3,2)
 d = (3,5)
 l = (1,6) - exit
 e
 t
 o
 d
 "

Maybe I could a map with frequencies going once through the array, then I go again check the letters and its frequecy. This would be O(n)!

hash map of input - O(n)
"a = 3
 c = 3
 d = 3
 l = 1 
 e = 3
 t = 1
 o = 1"

check the array again - O(n)

a - 3, skip,
a skip
c skip
...
l return index


### Code



```c++
int firstUniqChar(string s) {
    unordered_map<char,int> hs{};
    
    for(const auto &i:s) hs[i]++; // O(n)
    
    for(int i=0; i < s.size(); i++)
        if(hs.at(s[i])==1) return i; //n x O(1)
    
    return -1;
}
```
I need to go through the array at least   once to check if the first values repeats or not. The best possible runtime is a O(n) order


## Code 2.0 without maps

We fix an array with every letter, in theory the lookup time is faster in this case than a map.

```c++
int firstUniqChar(string s) {
    std::vector<int> v; hs(26);
    
    for(const auto &i:s) hs[i]++; // O(n)
    
    for(int i=0; i < s.size(); i++)
        if(hs[s[i]]==1) return i; //n x O(1) - here is faster
    
    return -1;
}
```