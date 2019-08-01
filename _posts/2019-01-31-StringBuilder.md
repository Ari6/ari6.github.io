---
layout: post
categories: [Java]
---

StringBuilder contatnation is much faster than String + concatination.

```java
public static void main(String[] args){
    //StringBuilder elapse
    long start = System.currentTimeMillis();
    StringBuilder sb = new StringBuilder();
    for(int i = 0; i < 100000; i++){
        sb.append("TestTestTest");
    }
    long end = System.currentTimeMillis();
    System.out.println("StringBuilder: " + (end - start) + "ms");

    //String +
    start = System.currentTimeMillis();
    String s = "";
    for(int i = 0; i < 100000; i++){
        s += "TestTestTest";
    }
    end = System.currentTimeMillis();
    System.out.println("String: " + (end - start) + "ms");
}
```

Result is

```
StringBuilder: 23ms
String: 12757ms
```

# Notes
I realized few things when I play around with StringBuilder class.

1. substring() returns String class object.
2. equals() does not work the way I thought. If you want to compare with String class, you need to do this below.

```java
StringBuilder sb = new StringBuilder("Test");
sb.toString().equals("Test");
```