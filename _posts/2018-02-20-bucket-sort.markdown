---
title: "Sort Algorithm"
layout: post
date: 2018-02-20 23:42
tag:
- algorithm
star: false
image: /assets/images/profile.jpg
headerImage: true
projects: false
blog: true
category: blog
author: Jianfeng
description: Notes for algorithm
externalLink: false
---

## Summary

I was wondering whether I should write blogs on these general algorithms. I know a lot of people are doing this, but I think everyone should write blogs based on their own knowledge. Afterall, general algorithms are well-known and open-source (and had been published by scientists many years ago).<br/>

I change my mind today - I will start taking notes on algorithms and other things that I've learnt. Why? 'Cause I start to forget how bucket sort works.

## What is Bucket Sort

This is the fastest sorting algorithm in the world. (Time: O(N); Space: ?) The bad thing is obvious. That is we can consume unlimited storage space.<br/>

Given: inputList = [3 5 2 10 5 8]<br/>
Req: Sort the integers in the increasing order<br/>

First, we create a list with length = max(inputList+1). For the above list, we have the list midList = [0 0 0 0 0 0 0 0 0 0 0] (length=11)<br/>

Second, we iterate through the inputList. During the process, for element 'cc', we have the following operation: midList['cc'] = midList['cc'] + 1<br/>
In our case, midList = [0 0 1 1 0 2 0 0 1 0 1]<br/>

Third, we iterate through the midList. For index=i, we output integer i for midList[i] times.<br/>
In our case, resList = [2 3 5 5 8 10].<br/>
Thus, we finish the sorting process.<br/>

## What can we do with Bucket Sort

When there are lots of duplicate elements in the inputList (the total number of elements in inputList is very limited), we can consider using Bucket Sort. It will give you O(N) time complexity, which is amazing.<br/>

For example, I look at this problem today: you are given a string, sort it in decreasing order based on the frequency of characters. At the beginning, I think I can use PriorityQueue, which can give us O(NlgN) time complexity. However, this is a good chance to use Bucket Sort.

## Implementation

{% highlight python %}
# Bucket Sort
def bucket_sort(input_list):
    res_list = []
    max_elem = max(input_list)
    midList = [0 for i in range(max_elem+1)]
    for elem in input_list:
        midList[elem] += 1
    for i in range(len(midList)):
        if midList[i] >= 1:
            res_list += [i for j in range(midList[i])]
    return res_list

print "Bucket Sort:", bucket_sort([1,3,2,4,8,6,5])

<Results>
terminal$ Bucket Sort: [1, 2, 3, 4, 5, 6, 8]
{% endhighlight %}

