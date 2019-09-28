Title: ASP.NET Core 3.0 Workshop
Tags:
  - community
  - workshop
  - aspnetcore
  - webapi
  - blazor
MetaImage: /images/2019-07/workshop-cover.png
---

![ASP.NET Core 3.0 Workshop](/images/2019-07/workshop-cover.png)

**UPDATE (September 29th):** The workshop sample and materials have been updated to the final version of .NET Core 3.0. All the missing pieces are implemented.

## Workshop content

0. [Session #0](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/00-prerequisites.md) - Prepare your environment by installing and configuring prerequisites
1. [Session #1](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/01-introduction.md) - An introduction to .NET Core and ASP.NET Core in form of presentations
2. [Session #2](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/02-tools-and-templates.md) - Working with .NET Core CLI tools and Visual Studio 2019, analyzing project templates
3. [Session #3](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/03-choosing-a-domain.md) - Choosing a domain to develop and creating user stories for it
4. [Session #4](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/04-project-initialization.md) - REST API introduction, creating Web API project, introduction to Postman and configuring git
5. [Session #5](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/05-domain-models-and-database.md) - Creating domain models, EF Core context and migrations
6. [Session #6](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/06-controllers-and-actions.md) - Creating view models and controllers, validation, error handling, using Postman
7. [Session #7](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/07-securing-api.md) - Securing API with JWT token based auth
8. [Session #8](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/08-testing-and-documentation.md) - Creating unit and integration tests, adding Swagger support
9. [Session #9](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/09-versioning-limiting-monitoring.md) - Versioning APIs, usage limiting, monitoring and creating health checks
10. [Session #10](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/10-blazor-client.md) - Introduction to Blazor and creating client-side Blazor client
11. [Session #99](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs/99-resources.md) - Resources and further reading

## Introduction

For quite some time, I was thinking about creating a workshop for ASP.NET Core. After some talks I had with members of [EESTEC](https://www.facebook.com/eestec.lcbanjaluka/) student organization and the management of [Seavus](https://seavus.com/), the idea started to shape up. My plan was to build something that could be reused for various events - for community organized events, inside the company, for conferences, and of course to be usable for others too.

After almost two months of sleeping less, preparing samples, writing instructions and having a first live workshop with students in duration of 10 days, there's finally something to share. The current version of workshop, with sample project and instructions, is available [on GitHub](https://github.com/miroslavpopovic/aspnetcore-workshop). I was heavily influenced by .NET Foundation's [presentations and workshops](https://presentations.dotnetfoundation.org/) and I even took some of the materials from there - parts of presentation, presentation template and the cover image for the workshop. Why not, [my user group](https://www.meetup.com/BLbitUG/) and myself are members of .NET Foundation organization. You [could be too](https://dotnetfoundation.org/get-involved)! :)

So, what is this workshop about? Other than ASP.NET Core 3.0 of course. Well, at the end, I have decided to go with Web API route. After the introduction to .NET Core 3.0 and ASP.NET Core and looking through the available templates, together with attendees, a domain is chosen and implemented as REST Web API. That API is then improved and finally consumed by frontend SPA application. To continue at the bleeding edge, we are not using JavaScript SPA frameworks like [Aurelia](https://aurelia.io/) (the best one out there ;)), React, Vue or Angular, but a completely new thing called [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/client)!

The workshop itself is split into 10 parts (for now). Each part has it's [own document with instructions](https://github.com/miroslavpopovic/aspnetcore-workshop/tree/master/docs). There is a [prerequisites](https://github.com/miroslavpopovic/aspnetcore-workshop/blob/master/docs/00-prerequisites.md) document that you can use to prepare your environment. If you want to present it to others, there's a [speaker notes](https://github.com/miroslavpopovic/aspnetcore-workshop/blob/master/docs/speaker-notes.md) document to remind you what should you go through during each part.

Note that both ASP.NET Core 3.0 and client-side Blazor are at the moment in preview phase. .NET Core 3.0 will launch in September during [.NET Conf](https://www.dotnetconf.net/) and client-side Blazor sometime next year. The workshop is updated to Preview 7, which [came out](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-0-preview-7/) a few days ago and has a go-live license. There are some things in workshop that could not be achieved with the current version. I still consider the workshop a work in progress, until the final versions of .NET Core 3.0 and client-side Blazor are out and the workshop updated.

You are welcome to use the workshop as you see fit. You can follow it by yourself, using the provided instructions. Or you could present the workshop to your friends, community or company. You could also create a derived version of workshop from it - in which case I would be grateful for an attribution :). I hope it will be useful.

I'm also interested in presenting the workshop as well as [giving regular talks](https://miroslavpopovic.com/speaking), so if you have something in mind, like a community event, conference, etc., let me know.

## Live workshop

At the end, here are some pictures from the live workshop we had in Banja Luka. Thanks [EESTEC](https://www.facebook.com/eestec.lcbanjaluka/), [Seavus](https://seavus.com/), [BLbit](https://www.meetup.com/BLbitUG/), [Bit Alliance](http://bit-alliance.ba/) and [ETFBL](https://etf.unibl.org/index.php/en/home) for the help in organizing the event! And of course, thanks to all attendees, you were great!

![ASP.NET Core 3.0 Workshop, Banja Luka](/images/2019-07/workshop-1.jpg)
![ASP.NET Core 3.0 Workshop, Banja Luka](/images/2019-07/workshop-2.jpg)
![ASP.NET Core 3.0 Workshop, Banja Luka](/images/2019-07/workshop-3.jpg)
![ASP.NET Core 3.0 Workshop, Banja Luka](/images/2019-07/workshop-4.jpg)
![ASP.NET Core 3.0 Workshop, Banja Luka](/images/2019-07/workshop-5.jpg)
