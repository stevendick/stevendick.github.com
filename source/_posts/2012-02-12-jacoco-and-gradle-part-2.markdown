---
layout: post
title: "JaCoCo &amp; Gradle - Part 2"
date: 2012-02-12 18:13
comments: true
categories: [Gradle, JaCoCo, Java]
---

This is a small follow-up on my [first post][1] on[JaCoCo][2] & [Gradle][3] that shows how to collate and report the code coverage for a multi-project build.

We've already seen the basics in part one. We still run JaCoCo during the unit testing, but now the unit testing happens once per Java project.

I decided to collect together the generated JaCoCo coverage files for generating the report, but I think this step could be cut out, but I haven't tried this simplification yet. Here's the code coverage run per project and the results copied to the root project's output directory using the projects' names as part of the new coverage file names:

{% gist 1809759 copy-jacoco-data.groovy %}

Now we can generate the report from the individual JaCoCo data files and include the source code for each project:

{% gist 1809759 generate-report.groovy %}

The final part is to wire up the dependencies. We can't generate the report unless all the sub-projects have finished copying the JaCoCo data files:

{% gist 1809759 coverage-report-dependencies.groovy %}

[1]: http://stevendick.github.com/blog/2012/01/22/jacoco-and-gradle/
[2]: http://www.eclemma.org/jacoco/
[3]: http://www.gradle.org