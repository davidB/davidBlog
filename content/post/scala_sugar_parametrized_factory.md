---
title: "Scala, sugar in Java : make a type parametrized factory"
description": ""
date: "2010-09-14"
categories: ["articles"]
tags: [ "tips", "sugar", "lang/scala"]
---
The basic code to create an instance from a Type parameter :

(full [source on github](http://github.com/davidB/scala_sugar_in_java/tree/master/src/main/scala/sandbox_sugar/) )
```
// Scala

def newOne[T]()(implicit m: Manifest[T]): T = {
  // assume T as a no-args constructor
  m.erasure.newInstance().asInstanceOf[T]
}

// sample call
val v = newOne[String]()
```

```
// Java

public <T> T newOne(Class<T> clazz) {
  return clazz.newInstance();
}

// sample call from java
String v = newOne(String.class);

// sample call from scala
val v = newOne(classOf[String])
```
