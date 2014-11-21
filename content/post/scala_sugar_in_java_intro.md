---
title: "Scala, sugar in Java : intro"
description: ""
date: "2010-06-15"
categories: ["articles"]
tags: [ "sugar", "lang/scala"]
---
Few days ago (one month) at the first meeting of PSUG (Paris Scala User Group), I notice that lot of member need a smooth way to explore, to learn and to use scala and why scala could be interesting.
As I can’t do lot of speech, I decide to start by writing some mini-articles… and first step was to [ReBoot](/posts/reboot) the personnal site/blog.

To try to achieve the goal, I’ll writing a serie of mini-article about scala for java developper, where I plan to expose syntax sugar and pattern, not all but enough to start **writing scala code, like java code but with scala sugar**.

In this serie (and the rest of the blog), I’ll  try to use the following tools and conventions :

*   maven 3.x / mvnshell to build project via cli (Command Line Interface)
*   eclipse (3.6) + m2eclipse (0.10) + scala-ide (2.8.0) + m2eclipse-scala
*   scala coding convention from : http://davetron5000.github.com/scala-style/

hope to be helpfull.

The first sugar :
* no declaration of exception in method signature
  => no need to wrap to match signature (dictated by interface, framework)
* remove ‘;’ at end of line
* type inference
  => no need to double write Type
```
// Java
public Xvz doSomething() throws AbcException {
  Xyz v = new Xzy(...);
  v.doStuff();
  return v;
}
```
```
// Scala (step 1)
public def doSomething() : Xvz = {
  val v : Xyz = new Xzy(...);
  v.doStuff();
  return v;
}

// Scala (step 2) : remove implicit syntax (public, ; , return)
def doSomething() : Xvz = {
  val v : Xyz = new Xzy(...)
  v.doStuff()
  v
}

// Scala (step 3 ) : type inference
def doSomething() = {
  Xyz v = new Xzy(...)
  v.doStuff()
  v
}
```
