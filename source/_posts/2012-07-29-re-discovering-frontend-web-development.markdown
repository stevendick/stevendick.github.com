---
layout: post
title: "(Re-)Discovering Frontend Web Development"
date: 2012-07-29 18:42
comments: true
categories: 
---

Ever since I did front-end development with C & X Windows in the mid 90's I've stuck to server-side development as a preference. Some ASP (no, not the nicer ASP.NET, but the original - &#42;shudder&#42;) in the late 90's was a brief detour, but it's been solidly server-side since.

We've all seen the trend towards applications migrating to the browser and the related resurgence of Javascript as a language.

Related to this, I've been working on a large application with a legacy Java Swing client for the last number of years and our attempts to modernise this with a service layer and a more ambitious change of client technology.

For various reasons we started with Flex at the tail-end of 2010, and for non-technical reasons, this approach was killed in late 2011 (no, not related to Adobe's foot-in-mouth moment of appearing to [shoot Flex in the head][1]).

If I was to make the decision today, I'd go with a pure web approach. While we don't have the luxury of doing the re-write at the moment, I do want to be ready with a recommendation on what we could use.

This leads to the TL;DR bit - holy shit! There's a lot of frameworks and libraries for doing modern web stuff. It's damn confusing and I'm sure there's plenty of right answers.

We want to build a web application, not a web site, so I was leaning towards the [single-page application][2] style. Gmail is a classic example of this style. I've also never been a fan of server-side templating - this maybe a side-effect of doing ASP all those years ago. I'd prefer to keep the services as a pure API unencumbered with presentation stuff.

I'll end this piece with a list of interesting libraries and frameworks I came across in my research and follow-up on what came next:

- [Extjs][3]
- [Smartclient][4]
- [Ember.js][5]
- [Backbone.js][6]
- [Knockoutjs][7]
- [AngularJS][8]

[1]: http://blogs.adobe.com/flex/2011/11/your-questions-about-flex.html
[2]: http://en.wikipedia.org/wiki/Single-page_application
[3]: http://www.sencha.com/products/extjs/
[4]: http://smartclient.com/
[5]: http://emberjs.com/
[6]: http://backbonejs.org/
[7]: http://knockoutjs.com/
[8]: http://angularjs.org/
