---
layout: post
title: "AngularJS"
date: 2012-10-01 20:14
comments: true
categories: [html5, javascript, angularjs, spa]
---

Getting back into web development is an overwhelming experience as I recounted in my last entry. After perusing [this][1] interesting comparison of the various MVC Javascript frameworks, I decided to look further at [AngularJS][2] (I'll just call it Angular from here on out).

Why Angular? I liked Angular's approach to HTML templating and the emphasis on testing. Only after someone else mentioned it, did I realise that Angular imposes no particular implementation on the model; many of the other frameworks impose an inheritence model.

Based on the quantity of links and Github watchers, [Backbone.js][3] appears to be the leader in this space, though I think the comparison might be rather superficial as Backbone is more limited in scope (by design) than Angular. Backbone is more at the library end of the scale and Angular is towards the framework end.

As part of my evaluation of Angular, I wanted to build some very minimal working code. I have a lot of experience with Java, but find Java (the language) frustrating for modern development. To increase the fun, I built the backend with Grails; the Java world's answer to Ruby on Rails. Grails will be a topic of another blog entry.

## The Domain ##

I work in finance, so the demo was around CRUD (I only did the RU bit for Angular) for managing trades, essentially the buying and selling of funds. It could be about CRUD for any thing as finance only impacted the name of the fields I was capturing, not the functionality of the demo.

## Learning ##

I find Angular's documentation adequate - nothing more. The API guide is complete, but often missing the 'why' and the 'how' of a feature. Experimentation is the name of the game -  something I assume anyone looking at an early-stage technology (in any area of IT) would be comfortable with.

I think the tutorial is the weakest part. I can't quite put my finger on why the tutorial doesn't work for me, but I didn't like it and skipped it.

Much more useful was the basic [Angular template project][4]. Clone it from Github and you're good to go with a minimal, working Angular app. Now you can experiment and see the results.

There's a Google group and IRC chat channel as well. I had the occasional hit on the Google group when searching for answers, but I never tried the IRC channel for help.

There's a good number of videos on Youtube from the Angular team from various presentations they've given. I'd also recommend looking at some of the shorter and more focused videos on implementing Angular, especially from [John Lindquist][8] - as a bonus you'll see John using [Webstorm][9], a pretty nice IDE for web development that I switched to half way through my two week investigation.

## What I Implemented ##

Because I don't have enough new moving parts in my exploration, I deployed the end result to [AWS (Amazon Web Services)][10] using a custom domain and added HTTPS support.

I'd already used Grails to generate scaffolding for a simple CRUD app for trade entry using server-side rendering, so I decided to replace the RU bit with an Angular implementation.

I'm assuming readers are at least vaguely familiar with the MVC pattern (and its many variants). At the end of the day I didn't have much code to get Angular using the JSON-based Grails server. A big part of this is Angular's [resource][11] abstraction that makes it simple to bind CRUD functionality to a REST-flavoured server.

One area Angular is not opinionated is the file structure of your project. Being recently returned to JavaScript, I don't currently have a good feel for what makes a logical and maintainable file layout for Angular's routes, controller, services and models. Looking at how others organise their projects will be an interesting learning experience.

## Security ##

This more a general topic for the SPA (Single Page Application) style of application. With server-side rendering of web pages, it's easy secure the HTTP end-points, but how to secure the XHR calls? Ultimately, this appears to be going the way of something like [OAuth2][5] with tokens added to every call, but I didn't want to add yet another new topic to my investigation. Maybe I could continue to use session-based security I get for free with Grails?

The problem: requesting a secured URL triggers an HTTP 302 Found response that is automatically handled by the browser and does the redirection behind-the-scenes. You asked for a list of trades in JSON? Have an HTML page for the login form instead!

The redirect-to-login-page-on-insecure-access pattern doesn't seem like a good fit for SPA apps. Looking at the HTTP responses, 401 Unauthorized seems a more fitting response. But how to handle this in Angular?

The Interwebs to the rescue! You can find a discussion and code for a solution [here][6] and [here][7]. Thanks to Witold Szczerba for sharing his solution. The solution uses Angular's interception feature to:

1.	fire an event when we receive a HTTP 401 response and remember what we were trying to request
1.	Other code listening for the event will dynamically show a login form
1.	authenticate and fire a success event
1.	request the original URL

It took me a few hours to get this working in my app, but it's always a nice feeling when you get the code to do what you want it to.

## Summary ##

All-in-all, I enjoyed my experiment with Angular.

What I liked:

* Declarative nature with the HTML fragments
* Lack of code to write
* REST/resource abstraction

What needs some work:

* Documentation
* Examples
* Composable views

 [1]: http://codebrief.com/2012/01/the-top-10-javascript-mvc-frameworks-reviewed/
 [2]: http://angularjs.org/
 [3]: http://backbonejs.org/
 [4]: https://github.com/angular/angular-seed
 [5]: http://oauth.net/2/
 [6]: http://www.espeo.pl/2012/02/26/authentication-in-angularjs-application
 [7]: https://github.com/witoldsz/angular-http-auth
 [8]: http://www.youtube.com/user/johnlindquist
 [9]: http://www.jetbrains.com/webstorm/
 [10]: https://www.fohf.com/app/index.html
 [11]: http://docs.angularjs.org/api/ngResource.$resource
