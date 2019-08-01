---
layout: post
categories: [Java, sort]
---

I want to note about Comparator and Comparable in sort. Comparator is one of Functional Interface that you can use Lambda expressions. Comparator has compare() which is an abstract method. I want to note that one thing I was really confused about. To be a functional interface, an interface must have **only one abstract method**. Comparator has multiple methods in the class. Comparable is technically functional interface as well because it has only one method, compareTo() but the official document does not mention it is functional interface.

# How to use Comparable

This is sort for Dog class. Ascendant sort with name length first, then ascendant sort with age. Implements Comparable interface and implement compareTo method. To use compareTo(), the class has to implements Comparable interface and declare compareTo in the class. In the method, you can define how to sort. This case, ascendant sort both name length and age. This result will be [“kitty”, 15][“kitty”, 25][“Doggie”, 10]. \*Kitty is a name of dog. Sorry for the confusing.

```java
public public class Main {
	public static void main(String[] args) {
		Dog[] dogs = new Dog[3];
		dogs[0] = new Dog("Doggie", 10);
		dogs[1] = new Dog("Kity", 25);
		dogs[2] = new Dog("kity", 15);

		Arrays.sort(dogs);
		for(int i = 0; i < dogs.length; i++){
			System.out.println(dogs[i].toString());
		}
	}

}

class Dog implements Comparable {
	String name;
	int age;

	public Dog(String name, int age){
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return this.name;
	}

	public int getAge() {
		return this.age;
	}

	@Override
	public int compareTo(Dog a){
		int returnCode = this.name.length() - a.name.length();
		if(returnCode != 0) {
			return returnCode;
		}
		return Integer.compare(this.age, a.age);
	}

	public String toString(){
		return "name: " + this.name + " age: " + this.age;
	}
}
```

# Why can Comparator be a Functional Interface?

Since these methods in Comparator class are overrode(equals()) or default / static methods (after Java 8) which are ignored when you use Lambda expression. My understanding is that default and static, and overrode are already implemented in the interface. So in Comparator’s case, Comparator has only one abstract method compare().

# How to use Comparator for sort()

 You can use Lambda expressions when you need to use Comparator class. This case second argument of Arrays.sort(). You can use this with ArrayList.sort(). In this case, sort name length ascendant, and age as descendant. So this result will be [“kitty”, 25][“kitty”,15][“Doggie”, 10].

```java
import java.util.Arrays;
import java.util.Comparator;

package basics;

import java.util.Arrays;

public class Main {
	public static void main(String[] args) {
		Dog[] dogs = new Dog[3];
		dogs[0] = new Dog("Doggie", 10);
		dogs[1] = new Dog("Kity", 15);
		dogs[2] = new Dog("kity", 25);

		Arrays.stream(dogs).sorted((a, b) -> {
			int returnCode = a.name.length() - b.name.length();
			if (returnCode != 0) {
				return returnCode;
			}
			return Integer.compare(b.age, a.age);
			}).map(Object::toString).forEach(System.out::println);

	}

}

class Dog {
	String name;
	int age;

	public Dog(String name, int age){
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return this.name;
	}

	public int getAge() {
		return this.age;
	}

	public String toString(){
		return "name: " + this.name + " age: " + this.age;
	}
}
```

# Comparator with comparing() method

You can use comparing() that returns Comparator<T> as sort order. sort() receives the returned Comparator and uses it as sort order. In this case, sort name length ascendant, and sort age descendant. I got stuck the same problem [here](https://stackoverflow.com/questions/30382453/java-stream-sort-2-variables-ascending-desending).

```java
public class Main {
	public static void main(String[] args) {
		Dog[] dogs = new Dog[3];
		dogs[0] = new Dog("Doggie", 10);
		dogs[1] = new Dog("Kity", 15);
		dogs[2] = new Dog("kity", 25);
 
		Arrays.stream(dogs).sorted(Comparator.comparing(Dog::getNameLength)
				.thenComparing(Comparator.comparing(Dog::getAge).reversed()))
				.map(Object::toString)
				.forEach(System.out::println);
	}
 
}
 
class Dog {
	String name;
	int age;
 
	public Dog(String name, int age){
		this.name = name;
		this.age = age;
	}
 
	public String getName() {
		return this.name;
	}
	public int getNameLength() { return this.name.length(); }
 
	public int getAge() {
		return this.age;
	}
 
	public String toString(){
		return "name: " + this.name + " age: " + this.age;
	}
}
```

I like stream but this is kind of complicated. Where I have to see is .sorted(Comparator.comparing(Dog::getNameLength).thenComparing(Comparator.comparing(Dog::getAge).reversed()). What this part does is sort with dog’s name length ascendant, thenComaring() gives next Comparator that  sort with age descendant.  \*If the array includes null, you may want to use filter() or nullFirst or nullLast. 

comparing receives function and return Comparator.

I leaned new thing that stream actually does not store the result. I need to lean how to store the result.

Categories: Java, sort