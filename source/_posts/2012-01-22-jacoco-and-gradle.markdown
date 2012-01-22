---
layout: post
title: "JaCoCo &amp; Gradle"
date: 2012-01-22 18:01
comments: true
categories: [Gradle, JaCoCo, Java]
---

There's a new kid on the block when it comes to code coverage in the Java world: [JaCoCo][1] (Java Code Coverage).
 
It comes from the guys who did the EclEmma plug-in for Eclipse after they decided it wasn't worthwhile to evolve the Emma code coverage tool (they are not the original developers). Instead they decided to start over and JaCoCo is the (ongoing) result.
 
We originally used Emma for the code coverage, but this stopped working when we started using [Lombok][1] to generate all the boilerplate code that Java needs. The next step was Cobertura. I've worked with Cobertura in the past and found the build integration brittle; you end up with either 0% or 100% coverage and no obvious errors. Luckily one of the other guys set Cobertura up with our Ant build so I didn't need to do it again.
 
Now I'm moving our build over to [Gradle][2] and wanted to look at how JaCoCo was progressing. I was pleasently surprised to find they've released, so I went looking for documentation on how to get this working with Gradle. No such luck and no-one to my knowledge has (yet) written a Gradle plug-in. After this, maybe I will.
 
JaCoCo does ship with Ant tasks and since Gradle includes Ant, it is very easy to use the tasks to get the work done.
 
My first problem was working out where to get JaCoCo. Maven Central seemed the logical source, but that version appeared to be missing the Ant task and wouldn't work with my Gradle script. I went for downloading JaCoCo and adding the Jar to my build project to solve the problem.
 
One difference with JaCoCo from Cobertura is it uses a Java agent to instrument the classes on loading; no longer do we need to post-compile instrument the class files. This seems a much cleaner way of doing things.
 
A quick bit of googling turned up the solution for specifying the agent argument when executing our tests in the Gradle build:

{% gist 1657770 junit.groovy %}
 
The first thing I do is add the JaCoCo jar to a new Gradle configuration, codeCoverage. This allows me to keep the JaCoCo Jar seperate from other compile and test dependencies.
 
I'm passing a number of arguments to the agent to control JaCoCo's behaviour:
 
1. `${configurations.codeCoverage.singleFile}`
2. `destfile=${buildDirName}/coverage-results/jacoco.exec`
3. `sessionid=HSServ`
4. `append=false`
 
Taking each of these lines in turn, we have:

1. Here I make use a new configuration, `codeCoverage`, to resolve the location of the JaCoCo Jar file.
 
2. JaCoCo writes the code coverage metrics to a binary file we specify here.
 
3. Identify the code coverage session. I haven't had any success in seeing this in the results.
 
4. Re-create the output file each time rather than appending to an existing file.
 
This is enough to generate the statistics, but it doesn't generate the report. For the report you need to do more work:

{% gist 1657770 generate-coverage-report.groovy %}

Phew! There's a lot going on here. This is where we make use of the Ant tasks that come with JaCoCo. Let's break it down a bit:

### lines 3 - 5

Define an Ant task for the JaCoCo reporting task.

### line 7

The output directory needs to exist before the report is run.

### lines 10 - 14

Point JaCoCo to the binary file generated from the test run.

### lines 16 - 26

The JaCoCo report needs access to the class and source files.

### line 28

Create an XML output file (this isn't needed if you're only interested in the HTML output).

### line 29

Create HTML report.

I link the HTML output in our [Jenkins][4] build (I'm not aware of a Jenkins plug-in for JaCoCo yet).

The Gradle build where I use JaCoCo is a multi-project build which gives us the added challenge of combining the results from each project into a single report, but that's for another blog entry...

[1]: http://http://www.eclemma.org/jacoco/
[2]: http://projectlombok.org/
[3]: http://gradle.org
[4]: http://jenkins-ci.org
