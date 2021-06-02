---
title: Static in Java
date: "2021-06-02T23:46:37.121Z"
description: "Static in Java"
---

There are static blocks, variables, static methods and static classes.

Why would we declare anything static?
=>When we declare members as static they can be accessed before object of class is created and one does not have to create an object reference
=>It can be considered as a predefined value one needs.(for cookie or cake holders used to bake the temperature at which they would bake perfectly has to be marked on the stencil rather than the user having to make multiple cookies/cake to check: cookie or cake being the objects here)
=>A Bank Application would apply te same rate of interest for different accounts in its corerespondence
=>Static is class level loads when jvm loads classes.

**_instance blocks are invoked before the constructors_**

```java
public class Test {
	// Java code to illustrate order of
	// execution of constructors, static
	// and initialization blocks

		Test(int x)
		{
			System.out.println("ONE argument constructor");
		}

		Test()
		{
			System.out.println("No argument constructor");
		}

		static
		{
			System.out.println("1st static init");
		}

		{
			System.out.println("1st instance init");
		}

		{
			System.out.println("2nd instance init");
		}

		static
		{
			System.out.println("2nd static init");
		}

		public static void main(String[] args)
		{
			new Test();
			new Test(8);
		}

}
```

```text
o/p:
1st static init
2nd static init
1st instance init
2nd instance init
No argument constructor
1st instance init
2nd instance init
ONE argument constructor
```

**_why instance blocks when we have constructors or vice versa?_**
To initialize some data before object creation
(thought constructors are prefered over instance block due to flexibility to instantiate with different parameters or no parameters)

**_Static blocks_**
When one needs some computation or processing before initialization of static variables or before class constructor execution or instantiation one can use static blocks. The execution in this block happens exactly once when class is loaded and not more than that irrespective of number of objects of class created.

**_Static variables_**
When there is a need of a single copy of variable needed to be shared amoung all objects at class level, like a global variable or a common key to a room then static variable can be used.
=>local static varaibles inside methods are not allowed throws a compiler error stating illegal modifier. Reason: static being a class variable meant in class level attempt of limiting the scope would violate the purpose of static by itself

```java
public class Static {
	static int k=0;
	static {
		int i=1;
		k++;
		System.out.println("static block execution" +i);

	}
```

=>Static blocks and variables are executed in the order in which they are specified in the program

**_Static methods_**
Static methods can be accessed before any reference or instance of class is created. It does not need an object for its access. Static can directly call other static methods and can directly access static data. They however would not be able to make reference to non static data, this and super

=>static variable can be mentioned as a common property and static method a way to commonly modify static variable. Say, all kids in a class have the same classname(static) but would have a different rollnumber incremented one after other(inside a static method)

**_Static classes_**
Top level outer classes cannot be static but nested inner classes can be static. Static class can be instantiated without outer class getting instantiated. Inner classes can access both static and non static memebers of outer class but static classes can access only static members of outer class.

```text
**_?is outer classes static by default?
_**?how can inner static class be instantiated without outer class insatntiation?can the same be done with inner classes?
```
