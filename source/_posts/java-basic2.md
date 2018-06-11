---
title: Java Part2--Interfaces, Lambda Expressions, Collections, and Generics
date: 2018-06-11 20:39:25
categories:
  - 技术日志
  - 语言
tags:
  -Java
---
### 摘要: Java Study
<!--more-->

## JAVA Basic
### Java : Interfaces, Lambda Expressions, Collections, and Generics

1. Interfaces are similar with abstract types but only contain public abstract methods
    1. All the methods in the interface are going to be public
    2. Can't have any implementation
    3. Any class thast implements an interface can be referenced using that interface
2. Java 8 has added default/static methods as a new feature, it fully implement methods within an interface
3. public class A(child) extends B(parent) implements C(interface), inheritence is the 1st priority
4. Anonymous inner classes is a class in place instead of in a peparate file.
   Some practice is strongly need
5. Generics
   1. Provide flexible type safty to your code
   2. Move many common errors from runtime to compile time
   3. Provide cleaner, easier-to-write code
   4. Reduce the need for casting with collections
   5. Are used heavily in the JAVA collections API
6. T->type; E->element; V->value; K->key; S&U repesent the 2nd or 3rd types
7. Type inference
   1. Syntax:
      1. There is no need to repeat types on the right side of the statement.
      2. Angle brackets indicate that tpe parameters are mirrored.
   2. Simplifieds generic declarations
   3. Saves typing
   4. Sample: CacheAny<string> myString = new CacheAny<>()
8. Boxing and unboxing:
    #### Sample:
    	Integer i1 = 10;
		Integer i2 = 10;
	   Integer i3 = 128;
	   Integer i4 = 128;
	   System.out.println(i1==i2); //True
	   System.out.println(i3==i4); //False
9. TreeSet(sorted unduplicated elements), Hashtable(synchronized, non-null), HashMap(null allowed, non-sync)
10. Dequeue is a collection which can be used as a stack or a queue.
11. Java Streams is a sequence of elements on which various methods can be chained
    1. Immutable
    2. Once elements are consumed, they are no longer available from teh stream
    3. A chain of operations can occur only once on a particular stream
    4. Can be serial or parallel
    5. Sample:
    tList.steram()
        .filter(t->t,getState().equals("CA"))
        .forEach(SalesTxn::printSummary);
12. Method References:
    1. Reference to a static method
    2. Reference to an instance method
    3. Reference to an instance method of an arbitrary object of a particular type
    4. Reference to a constructor
13. Builder pattern: static inner Builder--> define all the memeber you want  ---> 通过各个方法把我们要赋的值封装到 Builder的对象中，返回 this，这样就可以使用链式的结构 ---> 最后定义一个 build() 方法，创建目标对象，并且传入已经封装了各个参数的 Builder 对象。 ---> 目标对象定义一个参数为Builder对象的构造函数 ---> 赋值 完成创建目标对象
##### Sample:

```java

package javaPractice;
/**
 * @author xiaobili
 *
 */
public class buildPatternPeople{
	private String givenName;
	private String surName;
	public int age;
	private String address;

	//must static class for directly calling
	public static class Builder
	{
		//must initialized
		private String givenName;
		private String surName;
		
		//optional initialized
		public int age;
		private String address;
		
		public Builder(String param1, String param2)
		{
			givenName = param1;
			surName = param2;
		}
		
		public Builder age(int Param)
		{
			this.age = Param;
			return this;
		}
		
		public Builder address(String Param)
		{
			this.address = Param;
			return this;
		}
		//return the build pattern
		public  buildPatternPeople build()
		{
			return new buildPatternPeople(this);
		}
	}
	//main constructor initialized by builder
	private buildPatternPeople(Builder builder)
	{
		givenName = builder.givenName;
		surName = builder.surName;
		age = builder.age;
		address = builder.address;
	}
}
```
