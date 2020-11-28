---
title: Comparator or Comparable
date: "2020-05-08T22:40:32.169Z"
description: Which will you use when and why ?
---

Lets consider an Customer Object class.

```java
public class Customer{

	  private int Id;
	  private String name;
	  private String email;
	  private String phoneno;
	  private double cost;
	  private int quatity;
	public int getId() {
		return Id;
	}
	public void setId(int id) {
		Id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getPhoneno() {
		return phoneno;
	}
	public void setPhoneno(String phoneno) {
		this.phoneno = phoneno;
	}
	public double getCost() {
		return cost;
	}
	public void setCost(double cost) {
		this.cost = cost;
	}
	public int getQuatity() {
		return quatity;
	}
	public void setQuatity(int quatity) {
		this.quatity = quatity;
	}
	}
```

Say we have to sort the customers based on the id i.e some default sorting by which we want to sort the objects.
How would we do that? We would implement the Comparable interface. Comparable interface's **compareTo method** provides a **default sorting** functionality using which we can sort objects based on a **single attribute**.

Lets implement Comparable interface on the above class from **java.lang** package.

```java
public class Customer implements Comparable<Customer>{

	  private int Id;
	  private String name;
	  private String email;
	  private String phoneno;
	  private double cost;
	  private int quatity;
	public int getId() {
		return Id;
	}
	public void setId(int id) {
		Id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getPhoneno() {
		return phoneno;
	}
	public void setPhoneno(String phoneno) {
		this.phoneno = phoneno;
	}
	public double getCost() {
		return cost;
	}
	public void setCost(double cost) {
		this.cost = cost;
	}
	public int getQuatity() {
		return quatity;
	}
	public void setQuatity(int quatity) {
		this.quatity = quatity;
	}

	@Override
	public int compareTo(Customer customer) {
		return this.Id-customer.Id;
	}
	//the customer objects are sort in ascending order
	}
```

sort it using

```java
Collections.sort(array_of_customer_objects);
```

Now, lets say we have a requirement where we might have to sort the objects based on **multiple attributes**, 1-- based on Name, 2. based on cost he purchased . Here we do not changing the existing object class but create **seperate Comparator Class implementation**. We implement Comparator from **java.util** package in **an anonymous class**.

Lets add the implementations to sort the onbjects based on name and cost.

```java

import java.util.Comparator;

public class Customer implements Comparable<Customer>{

	  private int Id;
	  private String name;
	  private String email;
	  private String phoneno;
	  private double cost;
	  private int quatity;
	public int getId() {
		return Id;
	}
	public void setId(int id) {
		Id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getPhoneno() {
		return phoneno;
	}
	public void setPhoneno(String phoneno) {
		this.phoneno = phoneno;
	}
	public double getCost() {
		return cost;
	}
	public void setCost(double cost) {
		this.cost = cost;
	}
	public int getQuatity() {
		return quatity;
	}
	public void setQuatity(int quatity) {
		this.quatity = quatity;
	}

	@Override
	public int compareTo(Customer customer) {
		return this.Id-customer.Id;
	}
	//the customer objects are sort in ascending order

	public static Comparator<Customer> NameComparator=new Comparator<Customer>() {
		@Override
		public int compare(Customer o1, Customer o2) {
			return o1.name.compareTo(o2.name);
		}
	};
	public static Comparator<Customer> CostComparator=new Comparator<Customer>() {
		@Override
		public int compare(Customer o1, Customer o2) {
			return (int)(o1.getCost()-o2.getCost());
		}
	};
}
```

Similarly if we have to include more comparator classes to sort objects based on more attibutes we introduce comparators like we have done above.

To sort the objects we can do that using the following implementation:

```java
Collections.sort(array_of_customer_objects,Comparator_object
```

I hope above content has put light on most of the doubts one had on comparators and how to implement them.

That should be it for today.. Have a nice time exploring and learning.
