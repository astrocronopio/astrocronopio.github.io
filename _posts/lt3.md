---
layout: post
title: 3. Longest Substring Without Repeating Characters
categories: [Leetcode, cpp]
---


- Given a string s
- Find the lenght of longest *substring* without repeating characters

## Brute:

int answer = 0;
int min=0, max=0;
map word (char, index)

example: a pawkey w

1 - loop through the string
	min = 0, max=0
	word[(a,0)] max =1
	word[(a,0),(p,1)] max=2

	for (a,3) a is at 0, max=3
		answer = max - min - 1 = 2





## Bottlenecks:



## Better Algorithm


## Code

```c++
#include <string>
#include <unordered_map>


// Example "absc cl longer"
int lenghtOfLongestSubtring(std:string s){

}
```

