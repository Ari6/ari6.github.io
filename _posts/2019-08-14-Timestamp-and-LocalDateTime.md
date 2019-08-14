---
layout: post
comments: true
categories: [Java]
---

When I used LocalTimeDate and Timestamp, I got stuck some problem convert LocalTimeDate to Timestamp.

# Long story short
LocalTimeDate.MIN and LocalTimeDate.MAX should **NOT** be converted to Timestamp.
It returns an unexpected result.

# What I did

```Java
Timestamp.valueOf(LocalDateTime.MIN);
Timestamp.valueOf(LocalDateTime.MAX);
```

I expected that I could get max and min values of Timestamp, but...

Result
```
Converted MIN to Timestamp : 169087565-03-15 04:51:43.0
Converted MAX to Timestamp : 169104628-12-10 19:08:15.999999999
```

So it does not give you what you want. \* I assume that you want the max and min values of Timestamp.

I found later this below from Java document.

```
The precision of a Timestamp object is calculated to be either:
19 , which is the number of characters in yyyy-mm-dd hh:mm:ss
20 + s , which is the number of characters in the yyyy-mm-dd hh:mm:ss.[fff...] and s represents the scale of the given Timestamp, its fractional seconds precision.
```

Source: [Java document](https://docs.oracle.com/javase/8/docs/api/java/sql/Timestamp.html)

It seems that LocalDateTime.MIN and MAX are outside of the scope.

# Lessons I leaned
* Don't be too lazy. I should have created just another method. I tried to reuse method method(Timestamp start, Timestamp end).
* I should check the result when you convert class to another class.

Categories: Java
