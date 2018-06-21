---
title: "Data Structure and Algorithms: Graph"
layout: post
date: 2018-04-02 11:42
tag:
- algorithm
star: false
image: /assets/images/profile_2.jpg
headerImage: true
projects: false
blog: false
category: blog
author: Jianfeng
description: Notes for algorithm
externalLink: false
---

## Summary

I was wondering whether I should write blogs on these general algorithms. I know a lot of people are doing this, but I think everyone should write blogs based on their own knowledge. Afterall, general algorithms are well-known and open-source (and had been published by scientists many years ago).<br/>

I change my mind today - I will start taking notes on algorithms and other things that I've learnt. Why? 'Cause I start to forget how bucket sort works.

## Graph - Definition and Representation

## Related Algorithms

### Depth-First Search and Breadth-First Search
When there are lots of duplicate elements in the inputList (the total number of elements in inputList is very limited), we can consider using Bucket Sort. It will give you O(N) time complexity, which is amazing.<br/>

### Implementation

{% highlight python %}
# DFS
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

{% highlight python %}
# BFS
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

### Strongly-connnected Components

### Implementation

{% highlight python %}
# Strongly-connected Components
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

### Minimal Spanning Tree

### Implementation

{% highlight python %}
# Minimal Spanning Tree
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


### Shortest-path Algorithm

### Implementation
{% highlight python %}
# Bellman-Ford Algorithm
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


### Implementation
{% highlight python %}
# Dijkstra Algorithm
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


### Maximum-flow Algorithm

### Implementation
{% highlight python %}
# Shortest-path Algorithm
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

