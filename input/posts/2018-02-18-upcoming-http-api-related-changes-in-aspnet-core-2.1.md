Title: Upcoming HTTP API related changes in ASP.NET Core 2.1
Tags:
  - aspnetcore
  - api
  - apicontroller
---

Two weeks ago ASP.NET team [unveiled](https://blogs.msdn.microsoft.com/webdev/2018/02/02/asp-net-core-2-1-roadmap/) it's roadmap for ASP.NET Core 2.1 release. In addition to some highly expected features like new SignalR version, Identity changes and WebHooks, the things that I'm most excited of are Web API improvements. These changes are summed up in an initiative with a funny name - Project KodKod - and a goal "to make MVC into a opinionated, forward-thinking, batteries included framework for HTTP APIs".

![Project KodKod](/images/2018-02/aspnet-mvc-project-kodkod.png)

Ever since ASP.NET Web API was introduced, almost 6 years ago, it became THE way that I was working with ASP.NET. I used it mostly to build a backend for SPA applications and on a few API only projects. My experience of building APIs is summed up in a talk that I've been presenting on local conferences and user group meetings, called "Building production ready APIs with ASP.NET Core 2.0". The samples and the conference PowerPoint presentations can be found [on GitHub](https://github.com/miroslavpopovic/production-ready-apis-sample). As ASP.NET Core 2.1 is coming with a number of new API-related features, it could be a good time to update my presentation. So, let's see what are some of those features...

## HTTPS by default

While not really an API specific feature, it's something that is more or less a must for public facing APIs. When you create a new ASP.NET Core 2.1 project, the template will enable HTTPS by default. A default local certificate will be created during .NET Core SDK installation. There will also be a new tool for managing certificates that will probably be installed as global tool. Global tools are a feature similar to Node global tools which will enable creation and distribution of tools ecosystem via NuGet. You can read more about it on [.NET Core 2.1 roadmap](https://blogs.msdn.microsoft.com/dotnet/2018/02/02/net-core-2-1-roadmap/).

In addition to HTTPS by default, the template will also enable HSTS - [HTTP Strict Transport Security](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) protocol - which will prevent browsers to try HTTP address. HTTPS will be forced.

## Better Swagger / OpenAPI specification support

For a long time, Swagger was de facto a standard for describing RESTful APIs but there were other tools too. That changed last year when SmartBear Software, a company behind Swagger, [donated](https://swagger.io/blog/announcing-openapi-3-0/) Swagger 2.0 specification to the OpenAPI initiative. Today, it's known as [OpenAPI specification 3.0](https://www.openapis.org/) and it's backed up by all the big players in API space.

ASP.NET Core 2.1 will come with a new type - `ActionResult<T>` which will enable discoverability of the action result type, without the need for additional attributes that is required now to get the correct metadata.

Also, a new tool will be added for build-time OpenAPI generation - at the moment we have only runtime generation. More features are planned for future versions.

## `[ApiController]` attribute

This is my favorite new feature that will bring back some conventions we had in old ASP.NET Web API. Basically, you will decorate controller class with `[ApiController]` and MVC will be able to infer some defaults and do additional processing on your action methods. This is what we will have for start:

### Automatic model state validation

No need to write `if (!ModelState.IsValid) return BadRequest(ModelState);`. Validation will be done automatically before calling your action method.

One of the _best practices_ I've been preaching is [wrapping a response in an object](https://github.com/miroslavpopovic/production-ready-apis-sample/blob/44870228b8c9952ca33ee791d80aacfa4256b762/BoardGamesApi/Models/ApiResult.cs) that has properties like `Error` and `IsSuccessful` in addition to the actual data. ASP.NET Core 2.1 will introduce a validation error response in the shape of [RFC 7807](https://tools.ietf.org/html/rfc7807) standardized response, but you will be able to override it.

### Inferring defaults on action method parameters

One thing that we lost in transition from the old ASP.NET Web API were automatic recognition of the source for action method parameters. This is coming back in ASP.NET Core 2.1. `[FromBody]` will be default for complex types. `[FromRoute]` will be used when possible and otherwise `[FromQuery]`.

### Other

There are few more things that will be enabled with the new `[ApiController]` attribute. You can find more in depth review of this attribute in [a post by Filip W](https://www.strathweb.com/2018/02/exploring-the-apicontrollerattribute-and-its-features-for-asp-net-core-mvc-2-1/).

## Sample

To summarize, let's take a look at one of the action methods that I have in my presentation sample code, and how it would look like in ASP.NET Core 2.1.

```
// Sample: ASP.NET Core 2.0
[Authorize]
[Route("api/games")]
public class GamesController : Controller
{
    private readonly IGamesRepository _gamesRepository;

    public GamesController(IGamesRepository gamesRepository)
    {
        _gamesRepository = gamesRepository;
    }
    
    /// <summary>
    /// Create a new game from the supplied data.
    /// </summary>
    /// <param name="model">Data to create the game from.</param>
    /// <response code="200">Returns the created game.</response>
    [Authorize(Roles = "admin")]
    [HttpPost]
    [ProducesResponseType(typeof(ApiResult<Game>), 200)]
    public IActionResult Post([FromBody] GameInput model)
    {
        if (!ModelState.IsValid)
            return BadRequest(ModelState);

        var game = new Game();
        model.MapToGame(game);

        _gamesRepository.Create(game);

        var url = $"{Request.Scheme}://{Request.Host}/api/games/{game.Id}";

        return Created(url, game.WrapData());
    }       
}
```

```
// Sample: ASP.NET Core 2.1
[ApiController]
[Authorize]
[Route("api/games")]
public class GamesController : Controller
{
    private readonly IGamesRepository _gamesRepository;

    public GamesController(IGamesRepository gamesRepository)
    {
        _gamesRepository = gamesRepository;
    }
    
    /// <summary>
    /// Create a new game from the supplied data.
    /// </summary>
    /// <param name="model">Data to create the game from.</param>
    [HttpPost]
    public ActionResult<Game> Post(GameInput model)
    {
        // No model state validation code here, hooray!

        var game = new Game();
        model.MapToGame(game);

        _gamesRepository.Create(game);

        var url = $"{Request.Scheme}://{Request.Host}/api/games/{game.Id}";

        return Created(url, game);
    }       
}
```

## Conclusion

Since I haven't posted on my blog in a while, I felt obliged to share some of my thoughts on the current state of .NET (Core).

As a long-time ASP.NET developer, it's really nice to see how rejuvenated ASP.NET Core is rapidly improving with each version. At one moment, before .NET Core became a thing, it looked like .NET ecosystem became stale. Even I (an early proponent of .NET) have took [a foray into Node](http://javascriptkicks.com/articles/147418/learning-node-js-and-react-while-building-a-product).

.NET Core, .NET Standard and ASP.NET Core have brought back the hope for .NET developers in general. Open-source approach, multi-platform, beautiful C# language and a great performance could make ASP.NET Core a framework of choice and a force to recon in the server-side world. 

We could even see a full-stack C# (similar to full-stack JavaScript with Node). An experiment to create a client-side .NET web framework that's running in a browser via Web Assembly is now on ASP.NET team's [GitHub repository](https://github.com/aspnet/Blazor). To learn more about it, watch [ASP.NET Community Standup](https://www.youtube.com/watch?v=Ta_qXpXQqGQ) from two weeks ago.

_If you didn't know, ASP.NET Community Standups have a new home on YouTube, under the [.NET Foundation channel](https://www.youtube.com/channel/UCiaZbznpWV1o-KLxj8zqR6A/videos)._

Finally, after some struggle, the future of .NET looks bright!