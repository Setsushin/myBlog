---
title: Why you should always use "guard"
categories: 
- Technologies
tags:
- python
---

You must ever been tormented by multiple nested _if-else_ statements, like following:  
```
if (case1):
    if (case2):
        if (case3):
            do something
		else:
		    break
```

Yes, for poor linear thinking of the programmer, it's very natural.  
However, the fact is that even the author himself, he will forget all logics when he reviews after only a few days.  
So if you want to implement the above logic, it's strongly recommended to use "gurad", like this:  
```
if (not case1):
	break
if (not case2):
	break
if (not case3)
	break
do something
```
which makes everyone who is trying to continue working based on your codes happier.

