---
layout: post
categories: [Java, algorithm]
---

```java
int[] select_method(int[] a) {
	int out[] = new int[a.length];
	out = a.clone();
	int min = 0;
	int min_index = 0;
	for (int i = 0; i < out.length; i++) {
		for (int j = i; j < out.length; j++) { // To find minimum element
			if (i == j) {
				min = out[j]; // Set first number as the smallest
				min_index = j;
			}
			if (min > out[j]) { //if min is greater than other elements, change min to it
				min = out[j];
				min_index = j;
			}
		}
		
		for (int j = min_index; j > i; j--) { // To swap elements
				out[j] = out[j-1]; // 
		}
		out[i] = min;
	}
	return out;
}
```

I have separate finding minimum number and swap minimum and other elements. I thought I had to slide all other element so that I could use for as loop but I did not need to slide all element before the index where minimum was. What I had…

Categories: Java, algorithm