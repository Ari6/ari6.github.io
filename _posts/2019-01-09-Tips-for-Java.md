This is memo for programming quizes.


# Input
```java
Scanner sc = new Scanner(System.in);
while(sc.hasNext()){
	String str = sc.next();
}
```

next() reads the input until the space.

hasNext() returns true if Scanner has next item.

You can skip words if you set those up as delimiter.

```java
 String input = "1 fish 2 fish red fish blue fish";
 Scanner s = new Scanner(input).useDelimiter("\\s*fish\\s*");
 System.out.println(s.nextInt());
 System.out.println(s.nextInt());
 System.out.println(s.next());
 System.out.println(s.next());
 s.close(); 
```

Result:
>	1
>	2
>	red
>	blue

# List and array

## List to array
```java
List<String> strList = new ArrayList<String>(Arrays.asList("This","is","a","list."));
String[] strArray = strList.toArray(new String[strList.size()]);
```

## array to List
```java
List<String> strList = new ArrayList<String>(Arrays.asList("This","is","a","list."));
```

or

```java
List<String> strList = Arrays.asList("This", "is", "a", "list.");
```

# array to stream

```java
String strArray = new String[]{"This", "is", "an", "array."};
Arrays.stream(strArray).forEach(System.out::println);
```

or

```java
String strArray = new String[]{"This", "is", "an", "array."};
Stream.of(strArray).forEach(System.out::println);
```

**CAUTION**

When you use primitive type array, Stream.of() and Arrays.stream() return different types. Since Arrays.stream() has overloaded methods for each primitive type.

Stream.of()

|----------------------|-----------------|
| Modifier/Type        |Description      |
|----------------------|-----------------|
| static <T> Stream<T> | of(T... values) |
|----------------------|-----------------|

Arrays.stream()

```
|----------------------|------------------------|
| Modifier/Type        | Description            |
|----------------------|------------------------|
| static DoubleStream  | stream(double[] array) |
| static IntStream     | stream(int[] array)    |
| static LongStream    | stream(long[] array)   |
| static <T> Stream<T> | stream(T[] array)      |
|----------------------|------------------------|
```

Source : [https://docs.oracle.com/javase/8/docs/api/index.html](https://docs.oracle.com/javase/8/docs/api/index.html)