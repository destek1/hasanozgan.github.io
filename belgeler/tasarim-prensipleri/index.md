---
layout: page
title: Yazılım Mühendisliği Tasarım Prensipleri
tags: []
status: publish
type: page
published: true
meta:
  _edit_last: '2'
---

## Nesne Yönelimli Programlama Tasarım Prensipleri ##

### Class Design Principles (S.O.L.I.D) ###

* Single responsibility (SRP)
* Open-closed (OCP)
* Liskov substitution (LSP)
* Interface segregation (ISP)
* Dependency inversion (DIP)

### Package Cohesion Principles ###

* Reuse release equivalence (REP)
* Common closure (CCP)
* Common reuse (CRP)

### Package Coupling Principles ###

* Acyclic dependencies (ADP)
* Stable dependencies (SDP)
* Stable abstractions (SAP)


## YAGNI (You Ain’t Gonna Need It) ##

## KISS (Keep It Simple Stupid) ##

## DRY (Don’t Repeat Yourself) ##

## WET (Write Everything Twice) ##

## GRASP (General Responsibility Assignment Software Patterns) ##

## Curly's Law (Do One Thing) ##

## Favour Composition over Inheritance

Always favor composition over inheritance ,if possible. Composition allows to change behavior of a class at runtime by setting property during runtime and by using Interfaces to compose a class we use polymorphism which provides flexibility of to replace with better implementation any time.

## Programming for Interface not implementation

Always program for interface and not for implementation this will lead to flexible code which can work with any new implementation of interface. So use interface type on variables, return types of method or argument type of methods in Java.

## Delegation principle

Don’t do all stuff  by yourself,  delegate it to respective class. Classical example of delegation design principle is equals() and hashCode() method in Java.Benefit of this design principle is no duplication of code and pretty easy to modify behavior.

## Hollywood Principle (don't call us, we'll call you) ##
Dependency Injection yada Inversion of Control olarakta bilinir.

The Dependency Injection pattern is an implementation of Dependency Inversion principle. It says “Don’t ask for dependency it will be provided to you by framework“.

Advantages of Dependency Injection:
 - More Readable Code
 - Loose Coupling
 - More Testable Code
 - More Reusable Code
 
## Encapsulate What Changes

Only one thing is constant in software field and that is “Change”, So encapsulate the code you expect or suspect to be changed in future.

Benefit of this Design principle is that Its easy to test and maintain proper encapsulated code. If you are coding in Java then follow principle of making variable and methods private by default and increasing access step by step e.g. from private to protected and not public. Several of design patterns in Java use Encapsulation. Factory Design Pattern is one example of Encapsulation which encapsulate object creation code and provides flexibility to introduce new product later with no impact on existing code.

 
## Test Driven Development Tasarım Prensipleri ##

* Kalıtım (inheritance) yerine kompozisyon kullanılmalıdır.
* Static metot ve Singleton yapılar kullanılmamalıdır.
* Bağımlılıkların enjekte (injection) edilmesi, testleri kolaylaştırır.



