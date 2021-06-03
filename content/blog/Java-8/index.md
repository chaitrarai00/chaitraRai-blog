---
title: Java 8 Feature
date: "2021-06-03T23:46:37.121Z"
description: "Java 8 Features"
---
***Lambda***
Lambda was a way to bring in functional programing as a new Java paradigm. All code until then in Java were associated with classes and objects and piece of code couldn’t exist in isolation. To get a less complex and more readable, maintainable code functional programming was introduced. 

We will consider a piece of code written in versions before Java 8, say Java 7
```java
public interface Greet {
	public void perform();
}

```
```java

public class HelloGreeting implements Greet{

	@Override
	public void perform() {
		System.out.println("Hello Greeting You");
	}

}

```
```java

public class Lambda {
	
	public void greet(Greet greet) {
		greet.perform();
	}

	public static void main(String[] args) {
		Lambda obj=new Lambda();
		Greet greet=new HelloGreeting();
		obj.greet(greet);
	}

}

```

Here we are passing the greet object and hence through this finding an implementation of Greet interface that has the suitable perform() method. The Code is quite lengthy here. It would be great if instead of passing the Object one could actually pass action or function in isolation instead of objects.
This can be done as below from Java 8 just passing the action using a Functional Interface
Like previous example we need an Interface but this would be a Functional Interface. Meaning a SAM interface which means it should constitute of only a Single Abstract Method. The @FunctionalInterface is and optional annotation but it’s a good practise to use it so that anywhere in future the Interface’s purpose is known to be SAM.
```java
@FunctionalInterface
public interface Greet {
	public void perform(); //declare only one abstract method
	default void foo() {
		System.out.println("deafult defined method");
	}
	static void func() {
		System.out.println("another static defined method");
	}
}

```

Adding any other abstract method in this Interface would result in a Compilation error.
```java

public class Lambda {
	
	public void greet(Greet greet) {
		greet.perform();
	}

	public static void main(String[] args) {
		Lambda obj=new Lambda();
		obj.greet(()->System.out.println("Hello Greeting You"));
	}

}

```
The program can be reduced significantly using lambda. Here the representation is : 
(para)->{what need to be executed? statements;}
The parameters and statements can be of any number but the number abstract methods in the functional interface should be exactly one. Otherwise the lambda would not be able to be defined accurately and will get confused as to which method it should take into consideration.

```java

public class Lambda {
	
	public void greet(Greet greet) {
		greet.perform();
	}

	public static void main(String[] args) {
		Lambda obj=new Lambda();
		obj.greet(()->System.out.println("Hello Greeting You"));
		Add add=(a,b)->a+b;
		System.out.println(add.sum(2, 5));
		StringLength length=s->s.length();
		System.out.println(length.getlength("udgdfgfg"));
	}

}

interface Add{
	int sum(int a,int b);
}
interface StringLength{
	int getlength(String s);
}

```
Consider list of people and sort list by lastname, print all elements after sorting and print people that have lastname beginning with “C”.
***Ways to create lambda expressions***
•	Create a Functional Interface and a single abstract method declaration
•	Use out of the box functional interfaces provided in jdk if avaialable

Take a collection of person, sort it in terms of lastname, print the names in the soted order and the print the names only with C in the beginning of lastname.
Before Java8:
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class Main {

	public static void main(String[] args) {
		List<Person> people=Arrays.asList(new Person("Fudge","Cornelius"),
				new Person("Serious","Black"),
				new Person("Severus","Snape"),
				new Person("James","Potter"),
				new Person("Remus","Lupin"),
				new Person("Colin","Creevey"));
		Collections.sort(people,new Comparator<Person>() {

			@Override
			public int compare(Person o1, Person o2) {
				return o1.getLastname().compareTo(o2.getLastname());
			}
		}); //we create anonymous comparator class
		
		printconditionally(people,new Condition() {
			
			@Override
			public boolean test(Person p) {
					return true;
			}
			});
//we create anonymous condition class for our created condition interface
		
		printconditionally(people,new Condition() {
			
			@Override
			public boolean test(Person p) {
					return p.getLastname().startsWith("C");
			}
			});
//we create anonymous condition class for our created condition interface

	}
	
//	public static void printall(List<Person> people) {
//		for(Person p:people)
//			System.out.println(p);
//	}
//	
	public static void printconditionally(List<Person> people,Condition conditon) {
		for(Person p:people) {
			if(conditon.test(p))
				System.out.println(p);
		}
	}
	public interface Condition {
		boolean test(Person p);
	}
}

```

Minimising this humungous code using lambda ,Predicate and Consumer :
```java

import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Predicate;

public class Main {

	public static void main(String[] args) {
		List<Person> people=Arrays.asList(new Person("Fudge","Cornelius"),
				new Person("Serious","Black"),
				new Person("Severus","Snape"),
				new Person("James","Potter"),
				new Person("Remus","Lupin"),
				new Person("Colin","Creevey"));
		Collections.sort(people,(p1, p2)-> p1.getLastname().compareTo(p2.getLastname()));
		
		printconditionally(people,p->true,p->System.out.println(p)); //using Predicate Functional Interface
		
		printconditionally(people,p->p.getLastname().startsWith("C"),p->System.out.println(p));
	}
	
	
	public static void printconditionally(List<Person> people,Predicate<Person> predicate,Consumer<Person> consumer) {
		for(Person p:people) {
			if(predicate.test(p))
				consumer.accept(p);
		}
	}
	
}

```
***Java has provided Some common Interfaces for common method operations. Some of the mainly used once are Predicate, Consumer, Supplier and Function.***
=>Predicate: boolean test(Object parameter) – returns a boolean
=>Consumer: void accept(T t)- just accepts values returning nothing
=>Supplier: T get()- returns values of type T
=>Function: R apply(T t)- applies a particular function on an argument given and return new results

***Streams***
•	Consider it as giving out objects in stream like moving in conveyer belt in the airport
•	They are related to collections framework or collection of objects
•	Used to perform bulk operations and process objects of collections
•	Reduces code length
```java

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Main {
	
	public static void main(String[] args){
		
		List<Integer> list_num=List.of(2,4,5,6,7,3,1,9,8);
		//get a filter out of all even numbers from a list
		list_num.stream().filter(i->i%2==0).collect(Collectors.toList());
		//System.out.println(list_num.stream().filter(i->i%2==0).collect(Collectors.toList()));
		
		list_num.stream().map(i->i*i).collect(Collectors.toList());
		System.out.println(list_num.stream().filter(i->i%2==0).map(i->i*i).collect(Collectors.toList()));
		/*stream returns a stream of elements, 
		*filter takes in a predicate and return boolean result on the operation on it
		*map takes a function and applys it on all the elements on the stream
		*collect is a Terminal operation that at last collects the result obtained
		*/ 
		
		list_num.stream().sorted().forEach(System.out::println);
		//get a stream sort it and foreach of it do a syso
		System.out.println(list_num.stream().min((x,y)->x.compareTo(y)).get());
		System.out.println(list_num.stream().max((x,y)->x.compareTo(y)).get());
		//on the stream apply a min/max function using compareTo method and use supplier to get the result
		Stream<Object> empty=Stream.empty();
		//create an empty stream
		int array[]= {1,2,3,4,5};
		//Stream<Integer> stream=Stream.of(array);
		//make a stream with the array provided
		Stream.builder().build();
		//uses builder pattern to build a stream
		Arrays.stream(new int[] {1,2,3,4,5});
		//create stream of array using Arrays
	}
	
}

```
