---
layout: post
title: "Wonderful Surprise"
description: "Nice feedback on a C++ book I've toyed with"
category: 
tags: [feedback, C++, tdd]
---
{% include JB/setup %}
I started working on a book some time back on C++ and something like OOD or TDD
or some such theme. You can see its current state [here](http://schuchert.wikispaces.com/cpptraining.CppAndOodTheLeastYouNeedToKnow).
I did that because at the time I was teaching C++ to C programmers at NASA and
I wanted to have additioanl backround material for the students.

As you can see by the date, I haven't done anything with it lately. I did 
contact some publishers but nobody seemed very interested and, like with a lot 
of my side projects, I get bored easily (my biggest known weakness), and have 
not been doing anything with it.

Then at the end of June 2012 I get the following email (reproduced with 
permission but name left anonymous by request - note, not a native English 
speaker but clearly able to communicate nonetheless):

<blockquote>

I just read your WiP book "C++ and Object Oriented Design, The Least
You Need to Know" and just really wanted to say how glad I am I found
it.<br/>

I am lead programmer in small video game company (few years of
experience in C++) and just recently started to look into TDD. I was
really surprised that (as you also mention in your book) there are
virtually no serious resources on TDD in C++ and as much as C#/Java
examples can be helpful, C++ has its own set of challenges (as
usual;)) in that area.<br/>

Main reason I got interested in knowing TDD better was the fact that I
got more and more afraid to do changes in the system, so I really
wanted some kind of safety net from unit (regression) testing. But
thanks to your book I already made bunch of changes in the system I
would never thought of being helpful. I learned that what "Driven"
really means and I never thought I will change my way of designing C++
code so much after 3 days of reading. I can honesty say that last book
that influenced me that much was "Modern C++ Design" by Alexandrescu
few years back. I consider myself skilled C++ programmer, I use STL
and BOOST daily. Metaprogramming is also not a black magic to me when
necessary. Thing is, even tho I could probably describe most patterns
and its usage from GoF book I must admit that after reading your book
I am not sure I really ever got true OOP. It always felt kind of too
Java for me and not really suited for "Modern C++". Again, after your
book I feel very different, relieved even, It shows that C++ code can
be both modern and maintainable (I feel sorry for some of BOOST
maintainers).<br/>

To summarize: please, please finish it. Not only I must know the rest
of chapter 7 but outline of ch. 8 is like the worst cliffhanger ever!
I feel that book is really necessary. I know I would pay a lot to have
this on my shelve. And every next tome of it ;)<br/>

With new C++ standard there is so much more to discuss. For simplest
example: which of smart pointers would you use as a factory method
return type (in years I went from auto_ptr -> shared_ptr -> unique_ptr
-> back to raw ptr because of all the limitations that standard ones
impose)? How would move semantics affect your class design?

</blockquote>

This is probably the nicest feedback I have ever received and now I'm going to 
get back into writing the book. I've changed the title from "C++ and OOD" to 
"C++ and TDD" and I'm trying to get it ported to a better format for e-book 
distribution.

We had a little bit of an email conversation and he followed up with:

<blockquote>

sorry for the late response, I am swamped lately due to closing
release of the game I am coding and you Sir are are the reason for
quite a lot of this work actually as I was quite happy with the shape
of my codebase until I read your book :P<br/>

Seriously though, I am happy to do this because with every smallest
possible change I make, with every smallest test I add to the current
code I feel better (more confident) about the system. I just stared
with TDD game but I don't think there is a return for me at this
point. I know that tests can't prove correctness of my production code
but for me it is enough to know that it at least does what I expect it
to do, even if that expectation is flawed I like to know that it is
implemented correctly.</br/>

I am very happy to hear that you want to continue to work on your
book! C++ programmers need it. I need it ;) Why (imho) are Sutter's
and Mayer's books so popular? Because with C++ we already have way too
much to worry about everyday. There is so many ways to do things
"correctly" that it is often very hard for inexperienced (as myself)
programmer to pick one. That is why we need guidelines from the better
ones. Not a generic design pattern example (poorly) ported from Java
but a real C++ code. Heck, I am now even changing implementation of my
global registry of types (for Object class derivatives) because of
your book (based on your MathOperation registry of course). It was
actually very similar in basic concepts (macro for registration +
global map of typeid -> factory functor) but your testable
implementation is just so much better that I just could not sleep with
mine obvious crappy one. Btw I realize it is just about the concept
(client unknowingly uses default global registry) but current
implementation of global RegistrationMap is not thread safe in C++98
(fixed in C++11).
</blockquote>

Here's what this says to me: He has groked it. Just a few points that say that 
to me:
* "I know that tests can't prove..." - this just speaks volumes of pragmatism to me.
* "I don't think there is a return for me..." - it's the same for me, once I became test infected, writing automated tests was non-negotiable. TDD and test infected are not the same thing but I feel almost as strongly for TDD as I do for test infected.
* "I just could not sleep with mine..." - I've been there. In fact, last night I was reading a little bit planning to go to bed and ended up on the long side of 3 a.m 2+ hours later.

I want to give specific credit where it is due. The "MathOperation registry" 
he speaks of is based heavily on [CppUTest](http://sourceforge.net/projects/cpputest/). 
I copied what they did, figured out how to design it to make it testable, then 
how to build it up in an approachable order test-first (as opposed to 
test-driven), but the basic design is not mine. 

In any case, here I am getting back into some side work on C++ because of this
person. I had clearly let the work slide. Now I just have to finish a blog
entry as a guest blogger for Martin Fowler's blog and port all of that work!
