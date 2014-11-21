---
title: "Why I don't continue to use getter and setter ?"
description: ""
date: "2006-09-19"
categories: ["articles"]
tags: [ lang/java"]
---
It has been a long time, I’m looking for a solution to avoid the getter/setter boilerplate. I wanted a solution ready for jdk 1.5 (and if possible for jdk 1.4). And after some night (of reading, studing, try,…), I found not one solution but a combinaison of solution. **No need anymore to write or generate getXxxx() and setXxxx(…)**. I keep my code cleaner and clearer. :

* Use public attribute as property, instead of private attribute and accessor methods.
* When I use framework/lib that can't access property without get/set, I post-compile classes files with [GetAndSetAdder ](file:///home/dwayne/work/oss/getset/target/site/gasa.html)to generate basic public getter/setter on bytecode. This way, reflection based lib will continue to work. (It's a tool I wrote and publish)
* If I want to add behavior when properties are accessed, I use AOP to add extra stuff before/after reading/writing attribute.

Please have look at the [Faq](file:///home/dwayne/work/oss/getset/target/site/faq.html) to understand why it's a valid solution (I apply it on EJB3/JSF project), [description](file:///home/dwayne/work/oss/getset/target/site/introduction.html) of the problem and the solution, and also [others approaches]() to compare with. I expect that after exploring this solution (reading documentation, faq,...), you will ask yourself : **"Why do we continue to use getter and setter ?"**

Take a look at [http://alchim.sf.net/getset](http://alchim.sf.net/getset). Every comments are welcome.
