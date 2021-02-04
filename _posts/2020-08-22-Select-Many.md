---
layout: post
title: Select Many
categories: [Programming, C#]
tags: [SelectMany]     # TAG names should always be lowercase
---

.NET SelectMany extension method in short, **selects many items for each item**! that's it.

I know it wasn't enough but it is a good point to start with. if you give a glimpse to the [msdn page](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.selectmany), you can see there is 4 overloads for this method.

Let's go through shorset first, the method signature is :

{% highlight cs %}
public static IEnumerable<TR> SelectMany<TS,TR> 
(this IEnumerable<TS> source, Func<TS,IEnumerable<TR>> selector)
{% endhighlight %}


By investigating the signature, you can comprehend 3 main points:

1. SelectMany applies and plugs to IEnumarable of generic type TS.
2. you should define some function to **Select** and convert each of the TS typed items to **Many** of the TR types.
3. the final and returned value should be an IEnumarable of TR typed items.

(note: TR stands for result type and TS stands for source type)

Let's try it :
We have a list of father names each of which have many children :
{% highlight cs %}
var origin=new List<Tuple<string,List<string>>>(){
Tuple.Create("fath1",new List<string>(){"jimmy","catrina"}),
Tuple.Create("fath2",new List<string>(){"lance","andy"}),
};
var res=origin.SelectMany(source=>source.Item2).ToList();

foreach(var item in res){
Console.WriteLine(item);
}
/*
output is:
jimmy
catrina
lance
andy
*/
{% endhighlight %}

We just passed a function that converts input tuple to list of children and the result is list of all children.

Ok, lets find out how another overload works:

{% highlight cs %}
public static IEnumerable<TResult> SelectMany<TSource,TResult> (this IEnumerable<TSource> source, Func<TSource,int,IEnumerable<TResult>> selector)
{% endhighlight %}

The difference with the first overload is that the function accepts another input as integer. and it is the index, so we can use it for the output. note that index refers to TScource typed items. lets see how it works:

{% highlight cs %}

var res=origin.SelectMany((source,Fatherindex)=>source.Item2.Select(child=>Fatherindex+"<<"+child)).ToList();
	
foreach(var item in res){
	Console.WriteLine(item);
}
/*
output is:
0<<jimmy
0<<catrina
1<<lance
1<<andy
*/
{% endhighlight %}

What if i wanted to print father names alongside of his child name?
by using first overload we can do this:

{% highlight cs %}

var res=origin.SelectMany(source=>source.Item2.Select(child=>source.Item1+"<<"+child)).ToList();
/*
output is:
fath1<<jimmy
fath1<<catrina
fath2<<lance
fath2<<andy
*/
{% endhighlight %}
It traverses like a two dependent for loop.

Ok, let's think what will happen if we use another list instead of children's name, some predefined constant list. well things get interesting: 
{% highlight cs %}

var somelist=new List<string>(){"A","B","C"};
var origin=new List<Tuple<string,List<string>>>(){
Tuple.Create("fath1",new List<string>(){"jimmy","catrina"}),
	Tuple.Create("fath2",new List<string>(){"lance","andy"}),
};
var res=origin.SelectMany(source=>somelist.Select(alph=>source.Item1+"<<"+alph)).ToList();
	
foreach(var item in res){
	Console.WriteLine(item);
}
/*
fath1<<A
fath1<<B
fath1<<C
fath2<<A
fath2<<B
fath2<<C
*/
{% endhighlight %}

As you ca see, it is like a two independent nested loop.

Two other overload are somehow alike first two with more intemediate results that can be used to produce more detailed results.
<!-- Find out more by [visiting the project on GitHub](https://github.com/mojombo/jekyll). -->
