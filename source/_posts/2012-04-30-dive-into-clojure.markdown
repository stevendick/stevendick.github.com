---
layout: post
title: "Dive into Clojure"
date: 2012-04-30 18:01
comments: true
categories: [JVM, Clojure]
---

No, not a review of a Clojure book you've never heard of: Dive into Clojure, but more a play on words as I spent quite a bit of time reading [Clojure Programming][1] (not to be confused with [Programming Clojure][2]) while on a diving holiday in Egypt's Red Sea.

Before getting to the book I want to say I think O'Reilly's Safari Online is pretty terrible. Difficult to navigate and always pushing for you to take a paid subscription. It compares badly to The [Pragmatic Programmer][3] guys in managing your books online. I was annoyed that the epud version wasn't available until the book was finished (I regularly use the early access feature to technical books).

I did very little functional programming at University and what I did (ML), I didn't like and/or appreciate. Since then I've been programming in a variety of languages including C/C++, Visual Basic and, for the last 10 years, Java. All firmly in the imperative style.

I am always looking for tools to make my programming life easier and I've become increasingly frustrated with Java's verbosity and clumsy support for meta-programming.

Of the newer languages on the block, I've dabbled with Python, Ruby, Groovy, Scala and now Clojure. So far, Groovy had been the the alternative language that was usable in my day job as it can work as a companion to your Java code whereas I see the other languages as a complete replacement (though they can all run on the JVM).

Why Clojure? Why not? Clojure had 2 points that drew me to it: it's a Lisp and that has an air of mysticism attached to it since it comes from the dawn of the computer age and it's a functional language. Scala pitches itself as a functional/OOP hybrid; you're not forced to go functional and I felt I would benefit from using a functional-only style language.

Of the three authors (Chas Emerick, Brian Carper and Christophe Grand), I had come across Chas and Christophe in my web reading around Clojure.

The first part of the book goes into detail on the nuts and bolts of Clojure before getting to the functional and concurrency parts of the language.

The one thing that sold me on the book and spending more time with Clojure is the example of a functional approach to implementing [Conway's Game of Life][4].

Wow.

This was a real eye opener for me on the power of a functional style. The elegance of the solution is something for me to aspire to as I learn more of Clojure.

This is the first time I've explored macros in Clojure. Previously I suffered the double trouble of hearing that macros are complicated and a mind poisoned by the C/C++ usage of the word 'macro'. While I'm sure there's plenty still to learn about them, I'm starting to see the power and their usage.

I enjoyed the fact that the book goes into detail on practical things, such as database access, web programming and how to deploy things. All essential features of getting stuff working in the real world.

I heartily recommend the book.


[1]: http://clojurebook.com
[2]: http://pragprog.com/book/shcloj/programming-clojure
[3]: http://pragprog.com
[4]: http://en.wikipedia.org/wiki/Conway's_Game_of_Life
