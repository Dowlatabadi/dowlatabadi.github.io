---
layout: post
title: Derangement!
categories: [Mathematics, Combinatorics]
tags: [Derangement]  
toc: true
---

Let's assume we have three items called a,b,c and we know their natural order, each of them belongs to which place. a belongs to first place and so on..  

The only permution that all elements are in right place is a,b,c. Ok, let's see how many permution we can have:

3!=6 

What are all 6 permutions:
```r
* a,b,c
  a,c,b
  b,a,c
+ b,c,a
+ c,a,b
  c,b,a
```

What is specific about + signed permutations? 
They call it "Derangement" and that means all of the elements are displaced from the natural position.
ok now we want to count all of the derangements.it can be done by using inclution-exclusion principle, recursion thinking or counting exact displaced elements.

## Counting All Possibilities

```r
exactly 3 elements are displaced: 2
exactly 2 elements are displaced: 3
exactly 1 element is displaced: 0
exactly 0 element is displaced: 1

so D(3 elemnts)=2
```

## Using Inclusion-Exclusion Principle
```r
Count(a dp,b dp,c dp)=Count(a or b or c dp)[3!-1] - 3*Count(exact 2 inplace)[3*0]+Count(exact 1 inplace)[3]=2
```

## Recursive Counting

Lets assume we know `D(n-1)`, now we want calculate `D(n)`, clearly one element is added.

One derangement is like: `[][][][][][][][] {}` we can exchange new element with oe of the old elements. Therefore for every derangement we can have `(n-1)` new derangement: `D(n-1)(n-1)`. 
Can we have more derangements? yes we can assume a be in its natural place: `a[][][][][][][][]` and other elements are not, now if we exchange a and `{}` we still have a new derrangement. so we need to count `D(n-2)` and for each of them we can pick `a,b,..` as right element and finally replace {} with right one: `D(n-2)*(n-1)` 

Now we have: 
```r
D(n)=D(n-2)*(n-1)+D(n-1)(n-1)
```


And ofcourse we can also write recursive and brute force code to calc derangement.


