---
layout: page
title: "Chapter 1"
description: ""
---
{% include JB/setup %}
<h1>Introduction</h1>
I started using C++ and Smalltalk in 1989; C++ as a research assistant, 
and Smalltalk in an Object Oriented Languages Seminar, both at the University 
of Iowa. In the spring semester of 1990, while taking an advanced Operating 
Systems course, I made a decision to use C++ (C Front 1.1), not allowing myself
to fall back to “plan old C” until I understood C++. That was the first and 
luckily only time I didn’t finish a project. It was the first project of the 
course and it turns out I was trying to create objects with virtual member 
functions in shared memory, which was a no-no. In any case, I continued using 
C++ and Smalltalk for some years. My chances to use Smalltalk diminished 
faster than C++.

C++’s library, while meager, grew. The boost library came into existence and 
then became quite a substantial collection of classes. Many of those classes 
are useful, some esoteric and several make the language behave more like some 
people would like it to behave.

In 1997, I finally switched to Java on my 3rd attempt. I had tried prior to 
Java 1 with some success. Then about the time Java 1 was released I tried 
again. A few months after Java 1.02 was released, I finally decided to jump 
the C++ ship. So I stopped using C++ professionally in 1997. For several 
years I managed to not use it. I’d occasionally take a look but for the 
most part, I did not use it between 1997 and around 2007.

In 2007 I joined Object Mentor and several of the jobs involved working with 
large legacy C++ code bases. So I managed to start picking it up again. 
However, unlike my last time using C++, this time I had a few more years of 
design experience, large system development and support, experience with test 
driven development and myriad other experiences that made my approach 
substantially different.
<h2>Why this book now?</h2>
If that were the end of the story, then I would not have written this book. Even though I noticed that the approach to development with C++ was missing out on several modern ideas, I didn’t see a need. Then in mid-2010 my good friend David Nunn asked if I’d like to teach a C++ and Object Oriented Design class at NASA. Of course I said yes.

I did some looking around to try and find some material that included good Object Oriented Design principles, C++ idioms, modern design practices such as the use of Test Doubles for test isolation, etc. I did not find anything. I looked at the course that Object Mentor offered and it wasn’t quite what I was looking for either. I considered a few other avenues but in the end, I did not find anything that fitted the particular situation, so I built my own C++ class (for the 4th time actually).

I designed a course with the intention of introducing C++, the basics of Test Driven Development, basic design principles, deeper design principles and design patterns. All of this to be introduced through exercises. In my original course design I planned for 2 projects. I added a third “simple” problem at the front, which became the first problem as it blossomed into something at once simple and rich enough to cover much of the language my students needed to know to start becoming effective C++ programmers.

￼While teaching this class, I finally came to the realization that there really is not yet a book that covers learning just the part of C++ you need to know for Object Oriented Programming. I looked but I did not find anything that quite fit the bill. There are excellent books to be sure. Nothing like the focus I wanted. Additionally, the books available did not take the approach I’ve taken in this book; embedded exercises and deep dives into the language to provide additional context to what was happening in the problem.

I had a similar experience like this back in 1988 when, faced with having my students shell out over $100 USD for books on micro-computers (a term probably before most reader’s time), none of which the students would need after the class, I decided to write a book for a computer literacy course I taught at a local community college.

While the book was initially published in 1988, it grew. It went from about 110 pages to over 300 and was used for roughly 9 years before being ousted for something more appropriate. I hope that’s what happens with this book as well. I’d like to think that people learning C++ will stop learning all of the language and focus on learning how to effectively use the language. To me, that means not using much of the language’s power. At least as a first step towards learning C++, the subset I’ll cover is a good start. Learn how to do things somewhat cleanly, and then learn the guts of the language if you plan to write libraries or you just want to be a language nerd. C++ offers many opportunities to do so, but you don’t need to start there.
<h2>How is it different?</h2>
As the title suggests, I do not intend to cover all of the language. In fact, I’ll cover a comparatively small subset of the language and the standard libraries. Even so, that is not the primary difference. This book is meant to be an example of a journey through two problems.

The approach for each problem is similar; start with simple goals, write a solution. Review that and fix it as necessary. As I work through the solution, I’ll be articulating forces driving my decisions. I’ll be bringing into the mix things from C++, Test Driven Development, Refactoring, C, Test Isolation, Agile Software Development, etc.

Also, there will be two reasons why I cover something in the language. First and primarily, it will come up as a response to something in the current problem. Second, there will be background and context I might cover to fill out details a little bit. There will be times when I pick one solution over another to delve a bit more into the language or library. However, when I make that kind of decision, you’ll know because I’ll tell you.

Another key difference with this book is that I intend for you to write code as you work through this book. That, in and of itself, is not unique. What is, however, is that I’m going to provide you tutorials so that you’ll be able to write working code. Something that has always frustrated me is seeing code snippets with just enough context to get you interested but leaving “some assembly required” for the reader.

To address this, I have done three things:
* First, I have picked a tool set. It’s free and should be available on Windows, OS X and most UNIX varieties.
* Second, I have uniquely identified all of the tutorial sections with GUID’s (globally unique identifiers – that’s a geeky way of saying something obvious)
* Finally, I have included the same detailed instructions for other platforms online (http://schuchert.wikispaces.com/cpptraining)

To make this a bit easier, each tutorial section will cover mechanics at the beginning and then get into coding. As a result, there will be times where I have you do mechanics work ahead of time to reduce the number of unique times where you have to do that.

So even if you do not know C++, you should be able to get working examples. I hope that the text and code examples will enable you to pick up quite a bit of C++ along the way. I’ll be rewarding the ability to copy the provided code, however, with passing unit tests.

As a final difference, you’ll be running everything under the umbrella of a unit test. We will cover 2 projects. This means you’ll create two main programs. After that, all execution will be from tests written using a unit testing framework. I’ll provide both working code and failing code so you can see the errors. In some cases I’ll deliberately have bad designs; in some cases I’ll ask you to perform some experiments in your code. The experiments are a controlled way for you cause a failure, know why the failure happened, and know how to fix it. So rather than avoiding all errors, I’ll try to give you a chance to experience them in a safe manner.
<h2>What not to expect?</h2>
I’m assuming you have some basic background in C for reading this book. That’s really my target audience. I think you can use this book if you’re learning C++ from other languages, but I’m not going to make any wild guesses as to whether that will or will not work. If you are using C++ or learning C++, then you mostly likely have been using C in some capacity. I have not recently come across anybody learning C++ as their first language, so that is not what I am targeted. Having said that, I will be delving into C stuff every so often to explain why C++ is the way it is. You will be able to pick up this book and start programming in C++

Bottom line, you are not going to learn all of C++. In fact I’d guess you’ll learn maybe 30% of the language (I’m guessing at the number because a precise number without context isn’t of much value). However, of that 30% you do use, it’ll be what you need 90% of the time. The other 10% comes with practice, experience and the many references I’ll suggest to you later in the book.

This is the start of a journey. I hope it will set you on a good course and heavily influence your use and future learning of C++.
<h2>Standing on the Shoulders of Giants</h2>
The only thing I’m offering in this book is my particular combination of choices; there is nothing new in this material.

First and foremost, I need to give appreciation to several early influences in my software development career. My early interest in computers was fed by my friend John Navitsky. I was given a summer job by Marjorie Scriver working in a second-hand shop, which allowed me to earn enough money to buy my first computer. One week before I turned ￼18, Dr. Gretchen L. Moine hired me and some of my friends to work in a computer lab at Kirkwood Community College. When two of her professors left, she gave us the opportunity to teach computer literacy courses, and then like a mother hen, she defended us as the main campus tried to get rid of us. If I have any ability as a teacher, it is directly related to early, eager and consistent stewardship.

I had several good professors at The University of Iowa and one in particular got me started learning about OO programming, Dr. Mahesh Dodani. He offered an “Advanced Seminar in OO Programming” in the Fall semester of 1989. I used Smalltalk, but more importantly, because I took that class I was eligible to get a job as a research assistant developing a large C++ application. My friend Jeff Francis was instrumental in helping me with the C part of C++, and some of the basics, like using CVS. Unlike course work, we had to demo our work to Ford Motor Company and TACOM, so it was an amazing learning experience. I would not have started using C++ if not for Mahesh.

When I started using C++, Google did not exist and there were no books on C++. So when books came out, I bought them and devoured them. C++ is the invention of Bjarne Stroustrup. The first book I read on C++ was the original printing of The Annotated C++ Reference. The second book I read was by James Coplien, Advanced C++ Programming Styles and Idioms. Many books and articles followed. Anybody who’s read the work of Andrew Koenig will probably recognize his influence on my mental model of the language. Much of how I think about the language was certainly influenced by his book C Traps and Pitfalls and his many excellent articles in the C++ Report, many of which are available in Ruminations on C++.

James introduced me to book reviews. I purchased the first edition of his book Advanced C++ Programming Styles and Idioms. I read it and began an email conversation with him. As a result of giving him feedback, he connected me with his publisher and I ended up reviewing books. One of those books was Robert Martin’s first book Designing Object Oriented C++ Applications using the Booch Method.

There are many more, too many to remember. So I’m only bringing my perspective to material that already existed in other forms written by other people.

??? fill in? shorten? Move to appendix? ???
