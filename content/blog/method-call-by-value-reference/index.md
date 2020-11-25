---
title: Call by Reference or Value 🤔 in Java!
date: "2020-05-06T23:46:37.121Z"
description: "Call by Reference or Value 🤔 in Java!"
---

In this blog we will explore the Call by refernce and call by value in Java(Because that is my favorite 🤓).

The calls mentioned here are both the method calls.

For those with c ,c++ background similar lines of method by reference with address being passed between methods will not happen in java
Reason: Java do not support pointers. In Java reference refers to the way of accessing object

So diving in,
**Call by Value** means calling a method with parameter as a value. here, argument value is passed to the parameter. The modiciation done to parameters passed does not reflect in caller's scope(the calling method).
on other hand
**Call by Reference** means calling method via reference. The modification done to paramters passed refelects the callers scope and stays persistent. i.e., the original value is changed by the called method's modifications

Lets try to understand using an example:

```java
class CallbyValue{
  int value=0;

  void add(int value){
    value=value+10;
    //note that we do not return these values
  }

  public static void main(String[] args){
    CallbyValue cv= new CallbyValue();
    // before we call the method the value is 0
    cv.add(100);
    //after we call the method the value stays 0.
 }
}
```

Now we modify the same code to communicate using objects

```java
class CallbyReference{
  int value=0;

  void add(CallbyReference cr){
    cr.value=cr.value+10;
    //note that we do not return these values
  }

  public static void main(String[] args){
    CallbyReference cr= new CallbyReference();
    // before we call the method the value is 0
    cr.add(cr);
    //after we call the method the value changes to 10.
 }
}
```
