---
layout: post
categories: [Python]
---

This is from my old memo #1.

Python has nonlocal and global for controlling variable scope. I think I should avoid global and nonlocal without reasonable reason.

nonlocal allows you to access variables whih are located outside of normal scope.

```python
def nonlocal_test():
	x = "test"
	print("test: ", x)
	print("test: ", id(x))

def local_function():
	x = "local"
	print("local: ", x)
	print("local: ", id(x))

def nonlocal_function():
	nonlocal x
	print("nonlocal before: ", id(x))
	x = "nonlocal"
	print("nonlocal: ", x)
	print("nonlocal: ", id(x))

#call
nonlocal_test()

local_function()
print("test after local: ", x)
print("test affter local: ", id(x))

nonlocal_function()
print("test after nonlocal: ", x)
print("test after nonlocal: ", id(x))

```

Result
```
test: test
test: 4346585752
local: local
local: 4348326552 #<- different object from nonlocal_test()
test after local: test #<- this object was not changed by local_function()
test after local: 4346585752

nonlocal before: 4346585752 <- the same object as nonlocal_test().
nonlocal: nonlocal
nonlocal: 4347970416 #<- object is assigned “nonlocal”
test after nonlocal: nonlocal #<- This object was changed since nonlocal_function() used the same object.
test after nonlocal: 4347970416
```

This indicates that local_function() uses new object x in the function.
On the other hand, nonlocal_function() overwrote object x.

