---
layout: post
title: "Spring AOP"
description: "Quick overview of getting Spring Aop up and running"
category: 
tags: [spring, aop]
---
{% include JB/setup %}
<style type="text/css">
td, th {
  border: solid 1px black;
}
</style>
<h1>Introduction</h1>
Many years ago I worked with [AspectJ](http://en.wikipedia.org/wiki/AspectJ) on a project to improve a part
of an aging system. I wrote up some tutorials on that [here](http://schuchert.wikispaces.com/AspectJ+Self+Study).

Fast forward 5 or 6 years and on the project we're working on we have a few places where AOP would be handy. One
is metrics/logging related. We are using Spring 3 and component scanning, so I figured using Spring AOP is an
obvious choice. We are already using it (badly) in another part of the system, so we are not introducing any new
technology into our current stack.

This blog is about mechanics, rather than concepts. If you want concepts, I can recommend the aforementioned tutorials
or [AspectJ in Action](http://manning.com/laddad2/). I will make some observations about differences between "raw"
AspectJ and Spring AOP below.

<h1>What you need to do</h1>
You can find the latest version of all of this code on [github](https://github.com/schuchert/spring_aop).

This example uses Spring 3.1, though 2.5 or greater should work fine. One thing I like to see when reviewing code
examples is a list of the required dependencies. I started with an empty directory and created a maven project
from scratch rather than using an archetype. Instead of filling this page with all of those details, if are so
inclined, review the [pom here](https://github.com/schuchert/spring_aop/blob/master/pom.xml).

<h2>Enabling</h2>
To make this easy/possible, we need to inform spring that we are using AOP.
In addition, this example uses auto-discovery of spring beans. To make this
happen, I use the following applicationContext.xml file:

***applicationContext.xml***
{% highlight xml linenos %}
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context-3.0.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop-2.0.xsd">

    <context:component-scan base-package="shoe.example"/>
    <aop:aspectj-autoproxy/>
</beans>
{% endhighlight %}
<table>
    <tr>
        <th>Line</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>13</td>
        <td>Enable component scanning. This will search the classpath for
        any classes under the package shoe.example and auto-register (add
        into the spring factory) classes with any number of annotations.
        In my case, I'm using: @Component, @Repository, @Service.</td>
    </tr>
    <tr>
        <td>14</td>
        <td>Turn on Spring AOP. This will take any classes with the
        annotation @Aspect and apply them to any beans retrieved from the
        spring container. This includes beans looked up from the
        application context directly or using the
        annotations @Autowired or Inject.</td>
    </tr>
</table>

<h2>Basic Aspect</h2>
Now that AOP is enabled, we will create an @Aspect:

***InformEntriesAndExists.java***
{% highlight java linenos %}
package shoe.example;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;

import javax.ws.rs.Path;

@Aspect
@Component
public class InformEntriesAndExists {
    @Around(
            value = "@target(service) && @target(path)",
            argNames = "jp,service,path")
    public Object reportRestEndpoints(
            ProceedingJoinPoint jp,
            Service service,
            Path path) throws Throwable {
        return executeShell(jp, "rest endpoint");
    }

    @Around("@target(service)")
    public Object reportServiceEntry(
            ProceedingJoinPoint jp,
            Service service) throws Throwable {
        return executeShell(jp, "service");
    }

    @Around("@target(repository)")
    public Object reportResourceExecution(
            ProceedingJoinPoint jp,
            Repository repository) throws Throwable {
        return executeShell(jp, "repository");
    }

    private Object executeShell(
            ProceedingJoinPoint jp,
            String which) throws Throwable {
        System.out.printf("%s - start: %s\n", which, jp.getSignature());
        try {
            Object result = jp.proceed();
            System.out.printf("%s - finish: %s\n", which, jp.getSignature());
            return result;
        } catch (Throwable t) {
            System.out.printf("%s - failing: %s\n", which, jp.getSignature());
            throw t;
        }
    }
}
{% endhighlight %}
<table>
    <tr>
        <th>Line</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>12</td>
        <td>This is an aspect class. It includes information on how to
        select code to be augmented (pointcuts) along with the code that
        will be added (advice) to the targeted code.</td>
    </tr>
    <tr>
        <td>13</td>
        <td>This code will be auto-discovered by Spring</td>
    </tr>
    <tr>
        <td>15</td>
        <td>Around the execution of matching methods, apply this code.</td>
    </tr>
    <tr>
        <td>16</td>
        <td>Classes that implement the Service interface and the Path
        interface will have this code added to all of their public methods.
        Note that "service" here is a symbolic, named reference to a
        parameter passed into this method. This also gives the so-called
        advice code access to the annotation while it executes (assuming the
        annotation has been configured to be available at runtime).
        </td>
    </tr>
    <tr>
        <td>20</td>
        <td>The name "service" is of the fully-qualified java type: org
        .springframework.stereotype.Service and it is the annotation that
        will be used in selecting target classes.</td>
    </tr>
    <tr>
        <td>25</td>
        <td>Classes that implement the service annotation will have the
        following code added to all of their public methods.</td>
    </tr>
    <tr>
        <td>32</td>
        <td>Classes that implement the repository interface will have the
        following code added to all of their public methods.
        </td>
    </tr>
</table>

<h2>One of the informed classes</h2>
Spring applies the aspect to classes with certain annotations. Here is one
such class:

***SomeService.java***
{% highlight java linenos %}
package shoe.example;

import org.springframework.stereotype.Service;

import javax.inject.Inject;

@Service
public class SomeService {
    @Inject
    SomeComponent component;

    public void method1() {
        component.method1();
    }

    public void methodThrowingException() {
        throw new RuntimeException();
    }
}
{% endhighlight %}

Nothing in this class would suggest that it impacted by the aspect. If you are
using spring-aware IDE, then you might notice clues in the editor window that
this class is informed by an aspect.

<h2>Demonstrate the aspect</h2>
Rather than wonder if this works or not, here is a sample test that checks to
see if the apsect is correctly being applied at runtime:

***ExerciseAspectTest***
{% highlight java linenos %}
package shoe.example;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import javax.inject.Inject;
import java.io.PrintStream;

import static org.mockito.Mockito.*;

@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class ExerciseAspectTest {
    @Inject
    SomeComponent component;

    @Inject
    SomeRepository repository;

    @Inject
    SomeService service;

    @Inject
    SomeRestEndpoints restEndpoint;

    private PrintStream originalOut;
    private PrintStream streamSpy;
    public static final String ANY_STRING = anyString();

    @Before
    public void redirectOut() {
        originalOut = System.out;
        streamSpy = mock(PrintStream.class);
        System.setOut(streamSpy);
    }

    @After
    public void restoreOut() {
        System.setOut(originalOut);
    }

    @Test
    public void shouldProduceNoOutputForComponent() {
        component.method1();
        verifyZeroInteractions(streamSpy);
    }

    @Test
    public void shouldProductOutputForRepository() {
        repository.save(this);
        verify(streamSpy, times(2)).printf(ANY_STRING, ANY_STRING, ANY_STRING);
    }

    @Test
    public void shouldProduceOutputOnRestEndpoint() {
        restEndpoint.method1();
        verify(streamSpy, times(2)).printf(ANY_STRING, ANY_STRING, ANY_STRING);
    }
}
{% endhighlight %}

<h1>Conclusions</h1>
Spring AOP is a method-only oriented version of Aspect Oriented Programing.
It is possible to do more fine-grained AOP with Spring by actually using
AspectJ directly. However, for my needs that is not necessary.

If you have used other Aspect Oriented Programming tools,  you might be
surprised at the simplicity of some of the point-cuts. There are significant
differences between general AOP and what Spring offers:
1. Spring AOP only targets methods
2. Spring AOP only targets public methods
3. Spring AOP only targets objects retrieved from the application context
4. Will never target @Aspect annotated classes (too bad, it's fun to apply aop
at multiple layers, but crazy in production code)

If you are using Spring and using some of its features like declarative
transaction demarcation, then you are conceptually, and possibly literally,
already using AOP. While "raw" AOP never became mainstream,  it is heavily used
in may too sets and in several places you might not expect.


