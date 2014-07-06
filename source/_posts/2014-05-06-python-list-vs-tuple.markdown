---
layout: post
title: "Python: List vs Tuple"
date: 2014-05-06 19:21:00 +0900
comments: true
categories: Python
---

## Syntax

First of all, let's write down list and tuple syntax.
``` python
l = ["a", "b", 54, "hello"]		# This is a list
t = ("a", "b", 54, "hello")		# This is a tuple

i = (1)							# Be careful, this is an integer!
```
<!-- more -->
The minor differences between their syntax are square brackets [] and 
## Differences
### Size
Basically tuples are fixed size whereas lists are dynamic. Get ready with your terminal.
```python
l = list(range(1000))
t = tuple(range(1000))

l.__sizeof__() 		#9088
t.__sizeof__()		#8024
```
Tuple consumes less amount of memory so it slightly boost up performance. Yes, just a little bit.

### Mutability
Let's make it simple.
List  : Mutable
Tuple : Immutable
Let's make it more simple.
```python
l = ["a", "b", 54, "hello"]		# This is a list
t = ("a", "b", 54, "hello")		# This is a tuple

l[2] = "c"		# l = ["a", "b", "c", "hello"]
t[2] = "c"		# 'tuple' object does not support item assignment
					# l = ("a", "b", 54, "hello")				
```	
### Usage
Tuples or lists? It depends. But most of the time we use lists because of we can change it's value. However, there are time when tuples are just handy.
```python
l = ["Beautiful","ugly"]
t = ("Beautiful","ugly")

print "%s is better than %s" % l
#TypeError: not enough arguments for format string
print "%s is better than %s" % l
Beautiful is better than ugly
```
Yes tuples can be used for string structures. Another usage of tuple is that we can use it as a key in dictionary. For instance you want to create a dictionary that holds longitute/latitude as key and place name as value, tuple will be good for key.
```python
places = {
	(27.175015, 78.042155): 'Taj Mahal'
	(-13.163587, -72.545861) : 'Machu Picchu'
}
```
##Conclusion
+ Tuples are slightly faster than lists.
+ Most of time we use lists instead of tuples due to its mutability.
+ Tuples are great for string structure, dictionary key.

###Source
+ [http://www.sthurlow.com/](http://www.sthurlow.com/python/lesson06/)
+ [http://news.e-scribe.com/397](http://news.e-scribe.com/397)
+ [http://jtauber.com/blog/2006/04/15/python_tuples_are_not_just_constant_lists/](http://jtauber.com/blog/2006/04/15/python_tuples_are_not_just_constant_lists/)