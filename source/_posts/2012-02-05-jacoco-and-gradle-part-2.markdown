---
layout: post
title: "JaCoCo &amp; Gradle - Part 2"
date: 2012-02-05 18:13
comments: true
categories: [Gradle, JaCoCo, Java]
---

This is a small follow-up on my [first post][1] on[JaCoCo][2] & [Gradle][3] that shows how to collate and report the code coverage for a multi-project build.

We've already seen the basics in part one. The missing piece is collecting and merging the code coverage results *before* we generate the report:

*stick gist here*

[1]: http://stevendick.github.com/blog/2012/01/22/jacoco-and-gradle/
[2]: http://www.eclemma.org/jacoco/
[3]: http://www.gradle.org