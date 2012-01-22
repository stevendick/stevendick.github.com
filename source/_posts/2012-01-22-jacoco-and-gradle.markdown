---
layout: post
title: "JaCoCo &amp; Gradle"
date: 2012-01-22 18:01
comments: true
categories: [Gradle, JaCoCo, Java]
---

There's a new(ish) kid on the block when it comes to code coverage in the Java world: [JaCoCo][1] (Java Code Coverage).
 
It comes from the guys who did the EclEmma plug-in for Eclipse who decided it wasn't worthwhile to evolve the Emma code coverage tool (they are not the original developers). Instead they decided to start over and JaCoCo is the (ongoing) result.
 
We originally used Emma for the code coverage, but this stopped working when we started using [Lombok][1] to generate all the boilerplate code that Java needs. The next step was Cobertura. Now, I've worked with Cobertura in the past and found the build integration brittle: you end up with either 0% or 100% and no obvious errors. Luckily one of the other guys set Cobertura up with our Ant build so I didn't need to do it again.
 
Now I'm moving our build over to [Gradle][2] and wanted to look at how JaCoCo was progressing. I was pleasently surprised to find they've released, so I went looking for documentation on how to get this working with Gradle. No such luck and no-one to my knowledge has (yet) written a Gradle plug-in. After this, maybe I will.
 
JaCoCo does ship with Ant tasks and since Gradle includes Ant, it is very easy to use the tasks to get the work done.
 
My first problem was working out where to get JaCoCo. Maven Central seemed the l
ogical source, but that version appeared to be missing the Ant task and wouldn't work with my Gradle script. I went for downloading JaCoCo and adding the Jar to my build project to solve the problem.
 
One difference with JaCoCo from Cobertura is it uses an agent to instrument the classes on loading; no longer do we need to post-compile instrument the class files. This seems a much cleaner way of doing things.
 
A quick bit of googling turned up the solution for specifying the agent argument when executing our tests in the Gradle build:

<script src="https://gist.github.com/1657770.js?file=junit.groovy"></script> 
 
The first thing I do is add the JaCoCo jar to a new Gradle configuration, codeCoverage. This allows me to keep the JaCoCo Jar seperate from other compile and test dependencies.
 
I'm passing a number of arguments to the agent to control JaCoCo's behaviour:
 
* ${configurations.codeCoverage.singleFile}
 
Here I make use the new codeCoverage configuration to resolve the location of the JaCoCo Jar file.
 
* destfile=${buildDirName}/coverage-results/jacoco.exec
 
JaCoCo writes the code coverage metrics to a binary file we specify here.
 
* sessionid=HSServ
 
Identify the code coverage session. I haven't had any success in seeing this in the results.
 
* append=false
 
Re-create the output file each time rather than appending to an existing file.
 
This is enough to generate the statistics, but it doesn't generate the report. For the report you need to do more work:

<script src="https://gist.github.com/1657770.js?file=generate-coverage-report.groovy"></script>

Phew! There's a lot going on here. This is where we make use of the
 
Our Gradle build is a multi-project build which gives us the added challenge of combining the results from each project into a single report, but that's for another blog entry...

[1] http://http://www.eclemma.org/jacoco/
[2] http://projectlombok.org/
[3] http://gradle.org