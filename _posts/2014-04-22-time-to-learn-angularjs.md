---
layout: post
title: Time to learn AngularJS
tags: durandal angular frontend
redirect_from: "/time-to-learn-angularjs/"
---

A week ago, Rob Eisenberg [announced](http://eisenbergeffect.bluespire.com/angular-and-durandal-converge/) that the future version of [Duranda](http://durandaljs.com/)l will be called [AngularJS](http://angularjs.org/) 2.0. What seemed to be a late April 1. joke proved to be true. Rob joined AngularJS core team as a full-time external contractor and they are already on the way, building the web's most advanced framework.

This was a mind blowing news, at least for me. A little over a year ago, I chose Durandal to be my front-end framework of choice. Usually, I lean toward the most used framework / library, and Angular was (and still is) on the fire. Having widespread adoption and a huge community, Angular looked like a clear winner. 

However, there was Durandal, a small framework built by one of the most inspiring developers. It used [Knockout](http://knockoutjs.com/) library for data binding and just built an MV* framework around it. Since I was a long time Knockout user, Durandal was so natural and easy to start with.

As always, Rob (and other contributors) did an excellent job. I've always admired him, ever since I tried old [Caliburn](https://caliburn.codeplex.com/) MVVM framework for WPF. He bought me completely with an inspiring talk on [building your own MVVM framework](http://channel9.msdn.com/Events/MIX/MIX10/EX15) which later become [Caliburn.Micro](http://www.caliburnproject.org/), a framework without which I cannot think of doing any XAML based app.

The amount of code you **don't** need to write when using Caliburn.Micro in your XAML apps is simply astonishing. Convention over configuration at it's best. Bindings everywhere. No need for all those ceremonial code, like IDelegateCommand etc. that other MVVM frameworks have. Just write your plain and simple .NET code. Heck, it even had [coroutines](https://caliburnmicro.codeplex.com/wikipage?title=IResult%20and%20Coroutines&referringTitle=Documentation) since day 1, which are basically async/await pattern, way before Microsoft brought it to .NET framework. Amazing.

The same concepts are implemented in Durandal. Again, convention over configuration rules. There is a little to none infrastructure code you need to write in your view models / controllers. Just write simple JavaScript modules and let Durandal handle the rest. 

I used Durandal with success on a [private project](http://silverreader.com/) and also on several client projects at work, so I can consider myself as an intermediate user. Now I'll try to deep dive into current version of Angular, to gain a perspective on what to expect in Angular 2.0. It might be better to wait for 2.0 and start learning then, since there will be [considerable changes](http://blog.angularjs.org/2014/03/angular-20.html), but I'm a sucker for learning. Besides, I would like to compare the philosophies behind both frameworks before that.

Now if I could only think of some small project to play around with...
