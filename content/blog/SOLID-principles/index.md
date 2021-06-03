---
title: SOLID Principles
date: "2021-06-01T23:46:37.121Z"
description: "SOLID Principles"
---

SOLID Principles are necessary folr good Object Oriented Design. It is vital for coming up with loosely coupled applications. Tightly coupled applications are highly dependent classes one should avoid and loosely coupled classes makes the code more reusable, maintainable, flexible, stable and eady for new comers and revisting. SOLID Principle reduces tight coupling.
**S**ingle Responsibilty Principle
**O**pen/Closed Principle
**L**iskovs Substitution Principle
**I**nterface Segregation Principle
**D**ependency Inversion Principle

**_Single Responsibility Principle_**
**"A class should have only one reason to change"**
Each class should have single purpose/ job/ responsibilty.

Lets consider a fully fledged Book class

```java

public class Book {
	private String name;
	private String author;
	private String text;

	//getter and setters

	public void noofwords(String text) {
		//some logic
	}

	public void grammerCheck(String text) {
		//some logic
	}

	public void addpagenumber() {
		//some logic
	}

}

```

Now this does have the functionality a Book should be having but we add a method to print the book.

```java

public class Book {
	private String name;
	private String author;
	private String text;

	//getter and setters

	public void noofwords(String text) {
		//some logic
	}

	public void grammerCheck(String text) {
		//some logic
	}

	public void addpagenumber() {
		//some logic
	}

	public void printbooktoconsole() {
		//some logic
	}
}

```

This actually violates the single responsibility principle. The Book should have isolated principles and printing can be put ahead in a seperate class as below.

```java

public class BookPrinter {
	private Book book;
	//getter and setters

	public void printbooktopublish(Book book) {
		//some logic
	}

	public void printbookonothersources(Book book) {
		//some logic
	}

	public void printbooktoconsole(Book book) {
		//some logic
	}
}

```

This way we have a seperate Printer class olely for printing books which means its a single purposed class making it independent of the Book class.
Also we can enhance it to various functionality to print to console, mail it or log it anything!

**_Open/Closed Principle_**
**"Software Entities i.e. classes methods etc should be open to extension but closed to modification"**
One should be able to extend a class behaviour without modifying the existing class.

Say u have a Simple Guitar class

```java

public class Guitar {
	private String make;
	private String model;
	private int volume;

	//getter and setters
}

```

Suddenly a super cool guitar comes in demand and you want to add in new features. instead of modifying the existing once you create an extension of it so that the unpredicatable changes good or bad do not effect the existing guitars

```java

public class SuperCoolGuitar extends Guitar {
	private String flamedsparks;

	//getter and setters
}

```

**_Liskovs Substitution Principle_**
**"Derived classes or child classes Must be substituable for child or parent classes"**
intorduced by Barbara Liskov in 1987, tyhis principle states that the child of a parent classes should be usable instead of its parent without any unexpected behavior.

Say a Car parent interface

```java

public interface Car{
	void turnOnEngine();
	void accelerate();
	//getter and setters
}

```

You have these child classes MotorCar and ElectricCar

```java

public class MotorCar implements Car{
	void turnOnEngine() {
		//you start the engine
	}
	void accelerate();{
		//you accelerate it
	}
	//getter and setters
}

```
