Title: Recreating ASP.NET Core individual authentication views in client-side Aurelia app
Tags:
  - aspnetcore
  - aurelia
  - authentication
Published: 9999-01-01
---

So, that's a mouthful title. What do I want to achieve here?

![]()

When you create a new ASP.NET Core 2.0 MVC project using either `dotnet new mvc --auth Individual` or selecting appropriate options through Visual Studio's New Project dialog, a project will be scaffolded to include `AccountController` and `ManageContoller` along with their respective views. My plan is to remove all the views from the generated project except the home view, refactor `AccountController` and `ManageController` into simple API controllers and reimplement project layout inside Aurelia.

## But why?

Why not? It certainly looks fun :) 

There are multiple other approaches for having ASP.NET Core project with Individual authentication Aurelia frontend:
1. Leave default ASP.NET Core template, allow access to client side app via `/home/index` or some other URL that's under `[Authorize]` attribute
2. Use separate projects for server app and client app - this usually means that they would be served from different addresses (different domain / subdomain / port)
3. Modify the ASP.NET Core template by turning controllers into API controllers and replacing views with a client-side implementation
4. Any combination of the above
5. Not using ASP.NET Core default templates and implementing authentication differently (i.e. via IdentityServer 4 or some third party provider)
6. ...

There are pros and cons to each one. We are going with option 3. One benefit would be that you could define layout in one place only - inside Aurelia client-side app. It's always benefitial to have a single source of truth. Additional benefit would be that you would have an API for authentication that could be used from other clients. Although, be careful here, as some clients might have slightly different auth flows. We don't want security to suffer with this refactoring.
