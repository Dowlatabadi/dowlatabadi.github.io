---
layout: post
title: Lambda-Map-Filter-Reduce-For-C#!
categories: [Programming, C#]
tags: [Lambda Functions,Reduce,Aggregate,Where,Filter,List Comprehension,Python,C#]
mermaid: true 
---

Quick look at equvalents of usefull functionalities in c#:


|                   C#                   |                                Python                                |
|:--------------------------------------|:--------------------------------------------------------------------|
| **`Func`** <br>  x => x * x                      | **`Lambda function`** <br>  lambda x: x * x                                     |
| **`Select`** <br>  l1.select(x=>x*x)            | **`Map`** <br>  list(map(lambda x:x * x,l1)) **☰**  [x * x for x in l1]            |
| **`Where`** <br>  l1.Where(x=>x>10)              | **`Filter`** <br>  list(filter(lambda x:x>10,l1)) **☰**  [x for x in l1 if x>10] |
| **`Aggregate`** <br>  l1.Aggregate((x, y) =>x*y) | **`Reduce`** <br>  reduce(lambda x,y:x*y,l1)                                   |





