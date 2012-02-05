---
layout: post
title: "Gradle + Groovy + Spock + Windows == argh!"
date: 2012-02-05 14:29
comments: true
categories: [Gradle, Groovy, Spock, Windows]
---

We've all experienced the 'pleasure' of [Yak shaving][1]. This is the tale of my most recent one.

In porting our build to [Gradle][2] we recently found we'd missed one project as part of the multi-project build. Easy, we just add the project to Gradles `settings.gradle` and all will be well.

Nope.

Another project in the build fails and it has no obvious relation to the newly re-added project. WTF? Some error about `groovyc` (the Ant task for building Groovy code) has failed.

A bit of googling shows we've run up against the command line limitation on Windows (8K for XP onwards, only 2K for older versions). Bummer, but we can change the default Gradle behaviour to run the Groovy compilation in-process rather than spawning the compiler from the command line and encountering the problem.

That should work. Nope.

Now [Spock][3] is complaining that we've failed to process the annotations on all tests using Spock. This must be because we're running in-process and Spock's annotation processor isn't on the classpath.

Maybe adding Spock to Gradle's classpath fixes this new problem? Nope.

OK, back to googling around. [Stack Overflow][4] shows a workaround for problems of classpaths that are too long. Basically, replace the long classpath with an empty JAR containing a MANIFEST.MF that defines the real classpath. Sounds easy enough.

Does the pathing JAR solve the problem? Nope. The first problem with this solution is the lack of a clear description with examples of how this works. The classpath. The paths should be relative URLs (absolute paths appear to work on Mac OS X, but not Windows) from the point-of-view of the pathing JAR. I did this, but none of my classpath dependencies were found and no obvious reason why.

Argh! Back to Google. I eventually found a recent [bug][5] about the command line length problem with Groovy and a proposed patch (not yet accepted). I also raised a problem with the Gradle guys to see if anyone else could point out a workaround.

After giving it a day and no simple workaround appearing, I decided to try and apply the patch myself and build my own local Groovy. I used the 1.8.5 version of Groovy and manually applied the patch in Eclipse as the patch line numbers didn't match up to the source. Groovy recently moved to building with Gradle, so after cleaning up the `docs.gradle` file (it had diff markings in it, meaning it didn't work), I was able to build with Gradle. The build did report an error right at the end, but this was after the` groovy` and `groovy-all` JARs were produced, so that wasn't a problem.

Using the locally built Groovy did have one downside: I needed to provide the needed dependencies explicitly rather than relying on the transitive dependencies automatically being resolved, but that's a small price to pay.

So at last, the build works and I can leave that particular Yak alone.

[1]: http://en.wiktionary.org/wiki/yak_shaving
[2]: http://www.gradle.org
[3]: https://github.com/spockframework/spock
[4]: http://stackoverflow.com/questions/5434482/how-can-i-create-a-pathing-jar-in-gradle
[5]: http://jira.codehaus.org/browse/GROOVY-5024