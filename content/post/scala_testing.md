---
title: "Scala, choosing a test lib"
description": ""
date: "2010-09-29"
categories: ["articles"]
tags: [ "lang/scala", "tools/eclipse", "tools/maven"]
---
I note here, (partial) results for my testing tool research/evaluation.

Features :

*   required
    *   run for maven
    *   run from Eclipse via shortcut ( Alt+Shift+X   [ S | T | N | any ] )
*   I would like
    *   support single before/after for set of test (run once, eg : start/stop backend connection)
    *   ability to use [ScalaCheck](http://code.google.com/p/scalacheck/) to generate a set of test
    *   nice assertion syntax (support scala type)
    *   support for skip/pending test
    *   to have less dependencies (jar) ass possible

I create a sample project to try test/bdd lib : [prj-scala-only](http://github.com/davidB/prj-scala-only/)

To run test under eclipse, I follow the rules :

*   to be able to run test the project have to compile (fully), **required**
*   name the file same as test class (and package sould match directory layout)

To run test under maven : `mvn test` :

*   end filename with Test (or Suite =&gt; require custom configuration)
*   If testng jar is in the classpath, then [surefire](http://maven.apache.org/surefire/maven-surefire-plugin) (the maven plugin that run test) only run testng file, so in the final project I comment TestNG dependencies and test using it

[JUnit](http://junit.org/) 3/4 :

*   ![:-)](/img/icons/greenled.png)  Maven :
*   ![:-)](/img/icons/greenled.png) Eclipse : via JUnit Runner Plugin
*   ![:-/](/img/icons/yellowled.png) before/after : only on static method, not scala firendly (need to declare an object)
*   ![:-(](/img/icons/redled.png) scalacheck :
*   ![:-)](/img/icons/greenled.png) assert syntax : via mix of SpecsMatchers or org.scalatest.Assertions, or ShouldMatchersForJUnit,…
*   ![:-(](/img/icons/redled.png) skip support  : not found how to
*   my sample code :

    * [JUnitExtendSampleTest](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/JUnitExtendSampleTest.scala)
    * [JUnitAnnotSampleTest](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/JUnitAnnotSampleTest.scala)

[TestNG](http://testng.org/) :

*   ![:-)](/img/icons/greenled.png) Maven :
*   ![:-)](/img/icons/greenled.png) Eclipse : via TestNG Runner Plugin
*   ![:-)](/img/icons/greenled.png) before/after :
*   ![:-(](/img/icons/redled.png) scalacheck :
*   ![:-)](/img/icons/greenled.png) assert syntax : idem JUnit
*   ![:-)](/img/icons/greenled.png) skip support  : via beforeXxx, or annotation, or test dependency chain
*   my sample code :
    *   [TestNGSampleTest](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/TestNGSampleTest.scala.off)

[Specs](http://code.google.com/p/specs/) :

*   ![:-)](/img/icons/greenled.png) Maven : extends SpecificationWithJUnit, or mix with JUnit (see doc, or sample linked below)
*   ![:-/](/img/icons/yellowled.png) Eclipse : I can’t run Specs via JUnit Runner Plugin, or as scala application if I follow Specs’ documentation, But works if I use @RunWith
*   ![:-)](/img/icons/greenled.png) before/after :
*   ![:-)](/img/icons/greenled.png) scalacheck :
*   ![:-)](/img/icons/greenled.png) assert syntax :
*   ![:-)](/img/icons/greenled.png) skip support  :
*   my sample code :
    *  [SpecsSampleTest](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/SpecsSampleTest.scala)
*   documentation of the site as grow with version, may be, a little clean up should be done.

[ScalaTest](http://scalatest.org/) :

*   ![:-)](/img/icons/greenled.png) Maven : extends JUnitSuite, or use @RunWith, or extends TestNGSuite
*   ![:-)](/img/icons/greenled.png) Eclipse : via JUnit Runner Plugin
*   ![:-)](/img/icons/greenled.png) before/after : via trait BeforeAndAfterAll/FixtureSuite, but not as friendly (IMO) as TestNG (failure in before =&gt; skipped test and not an error that stop every test)
*   ![:-)](/img/icons/greenled.png) scalacheck : detect pass/fail with JUnitSuite
*   ![:-)](/img/icons/greenled.png) assert syntax : several syntaxes
*   ![:-/](/img/icons/yellowled.png) skip support  : a pending are converted into failure for JUnitSuite and TestNGSuite, but are ignored in FunSuite
*   my sample code :
    *   [ScalaTestJUnitSuite](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/ScalaTestJUnitSuite.scala)
    *   [ScalaTestTestNGSuite](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/ScalaTestTestNGSuite.scala.off)
    *   [ScalaTestFunSuite](http://github.com/davidB/prj-scala-only/tree/master/src/test/scala/samples/ScalaTestFunSuite.scala)
*   The documentation is in the scaladoc

I stop here, my evaluation. But If you’re interested to continue, there is other solution like [Specsy](http://github.com/orfjackal/specsy), [ScalaTestCase](http://www.kotek.net/blog/junit3_scala_testcase), assert from [Scalaz](http://code.google.com/p/scalaz/),…

Conclusion :

I started this comparison because I was not able to use Specs under Eclipse, and to eval alternative. But at the end of the eval I found how to run Specs under eclipse.
And I don’t like a lot the too many syntax of ScalaTest (Error when before failed).
So currently, I’ll continue to use Specs.

I hope my feedback could help you.
