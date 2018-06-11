---
title: Java Part1--Java technology, syntax and class review 
date: 2018-06-3 21:52:25
categories:
  - 技术日志
  - 语言
tags:
  -Java
---
### 摘要: Java Study
<!--more-->

随着公司的在线课程，回顾下JAVA的一些基本常识，需要尽快把这个缺口补一下。里面还有些例子待补充

## JAVA BASIC--1
### Java technology, syntax and class review 
1. Number Literal: Any number of underscore character(_) can appear between digitals in numberic field
2. Case sensitive
3. String dontDothis = new String("bad practice") // this may create many instance which is needless in one loop
4. Good practice to use full package and class name
5. 'Super' key word is used to call a parent's constructor
6. JAVA only support single inheritence, a class only extend one other class
7. class scope.jpg
8. Overloading: some practice need: 1)overload child class without virtual both in java and C++; 2)change the access property from private to public or from public to private
9. 'Instance of' used to identify the class type of instance during run time
10. all class are subclass to 'Object'(java.lang.Object)
11. Three function need consider when override: Tostring, hashCode, equal
12. Static members can not access non-static members within the same class<test>
13. Static varialbles can be accessed even if class they are declared in has not been instantiated<test>
14. Avoid using an object reference to access a static variable
15. static initializer block is a code block prefixed by the static keyword <exmaple> 
16. Take care when using static import or should use it less
17. When a child class inherits an abstract method, it's inheriting a method signature, but there's no implementation or code behind it 
18. An abstract class may have any nuber of abstract and nonabstract methods.
19. When inhteriting from an abstract class, you must do the following(both):
    1) Declare the child class as abstract
    2) Override all abstract methods inhterited from the parent class. Failure to do so will result in a compile-time error.
20. Final method/class/variable, prevent multi-thread access and thread safe
21. Final references must always reference the same object but the contents of that boject may be modified
22. Nested class is a class declared within the body of another calss.Nested classes:
    Multiple categories:
        Inner classes
            Member classes
            Local classes
            Anonymous classes
        Static nested classes
23. Nest class are commonly used in applications with GUI elements
24. Nest class can limit utilization of a "helper class" to the enclosing top-level class
24. Enum's constructor can't be public or protected
25. Java final key word also could be used for parameter





