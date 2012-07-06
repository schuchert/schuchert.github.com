---
layout: page
title: "Chapter2"
description: ""
---
{% include JB/setup %}
<h1>Obligatory Hello World</h1>
Traditional language books often cover a so-called hello world "application." Just for completeness, here you go:
{% highlight cpp linenos %}
#include <iostream>
int main(int argc, char *argv[]) { 
	std::cout << “Hello World” << std::endl; 
	return 0;
}
{% endhighlight %}
However, that’s the last example of code that doesn’t include some form of self- validation. Throughout this book I’ll be using a unit testing framework in lieu of a main() program. You won’t see much explicit output either. You are welcome to add output yourself, but I’m going to rely on programmatic execution and validation.

This section covers the “hello world” meme, unit test style. That’s what the rest of this section covers.
<h2>Setting up your environment</h2>
<h3>The Tools</h3>
For this book, I will be using the following tool set:
* Eclipse CDT1
* Wascana Eclipse Plugin
* CppUTest

The first tool is our IDE2 and it requires that you have a Java VM3 installed. The second is a plugin to Eclipse that gives you a complete C++ tool set. The final item is a library that gives you support for writing automated tests. It is called a unit test framework, but its ability to assist in writing automated tests is, for my purposes, its most important feature.

I have chosen these tools for several reasons:
* They are all free and open source
* They work cross platform
* They give a consistent way to work across those platforms – other than default shortcut keys
* In the case of CppUTest, it does basic memory leak detection out of the box. 

Since you are reading this book to learn C++, something helping with memory leak detection is an important feature.

What follows are detailed steps for installation of these tools.
<h3>Installing the Java Developers Kit (JDK)</h3>
Download the Eclipse CDT from [here](http://www.eclipse.org/cdt/). This book was written using 7.0 of the Eclipse CDT, which is based on Eclipse Helios. Older versions may work; newer versions almost certainly will work.

You will be downloading a zip file. You can safely unzip it anywhere. You will only need to know where you downloaded it for two reasons:
* Primarily, you’ll be running it, so you’ll need to find the top-level executable
* One time only, you may be using programs installed underneath the eclipse directory, added by an Eclipse plugin.

To keep everything self-contained, I’ll be storing everything under a directory called learncpp. This avoids spaces in paths and it will make it easier to find everything you do. If you choose to use a different directory, make sure to replace learncpp with the directory you used. Here are two example full path names for an idea of just where I’m putting things:
* Under windows:<i> <b>C:\learncpp</b></i>
* Under OS X:<i> <b> ~/learncpp</b></i>

If you extract the Eclipse CDT zip file to learncpp, it will create:
* Under windows:<i> <b>C:\learncpp\eclipse</b></i>
* Under OS X:<i> <b> ~/learncpp/eclipse</b></i>

<h3>Starting the Eclipse CDT</h3>
Now that you’ve installed Eclipse, you can start it. Double-click on the eclipse application under the eclipse directory. When you do, you will be asked to provide a location for a workspace:<br/>
![select workspace location](/CppTdd/images/image001.gif)
