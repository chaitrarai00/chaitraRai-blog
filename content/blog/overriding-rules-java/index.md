---
title: Overriding in Java
date: "2021-06-11T23:46:37.121Z"
description: "Overriding rules"
---

In any OOP language, overiding is a feature that allows a subclass or child to implement a meethod that is already provided by it super class or parent class( just declared or defined too).
##When the method in subclass has the following values same as in it super class its said to override the method in super class

> > the same name,
> > same parameter,
> > same signature,
> > same return type

###Method Overriding is done to achieve RUntime Polymorphism###

The version of method that is invoked is decided by the object used to invoke the method. If a parent class object is used to invoke the method then method in parent is called , if child class object is used to call that method then method in child class

```java
class Parent{
    public void m1(){
        System.out.println("Parent method");
    }
}

class Child extends Parent{
    @Override
    public void m1(){
        System.out.println("CHild method");
    }
}


class Main {
	public static void main (String[] args) {
	    Parent obj1=new Parent();
	    Child obj2=new Child();
	    obj1.m1();
	    obj2.m1();

	}
}
```

```java
Parent method
CHild method
```

##Points in breif

> 1.  Access modifiers while overriding
>     the access should not reduce in child class
> 2.  Final methods cannot be overridden

> 3.  Static methods cannot be overriden (method hiding can happen)

> 4.  Private methods cannot be overridden

> 5.  overriding method should have same return type (invariant) or subtype (covariant)

> 6.  invoking overriden methods from parent in subclass

> 7.  constructors cannot be overridden

> 8.  exception handling during overriding
>     rule 1 : if parent do not throw exception then throw only unchecked exceptions in child
>     rule 2. if parent throw an exception then the child should either throw the same eception or child of it
> 9.  abstract method overriding
>     abstarct needs to be overriden
>     10.overriding and sychronized/strictfp
>     no effect on then

**https://www.codejava.net/java-core/the-java-language/12-rules-of-overriding-in-java-you-should-know**

**https://www.geeksforgeeks.org/overriding-in-java/**
**https://www.geeksforgeeks.org/using-final-with-inheritance-in-java/**
**https://www.geeksforgeeks.org/covariant-return-types-java/**
