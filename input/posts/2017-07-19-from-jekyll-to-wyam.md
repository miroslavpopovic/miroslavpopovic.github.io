Title: From Jekyll to Wyam
Tags:
  - blog
  - jekyll
  - wyam
---

## Back to .NET

After doing mostly JavaScript development in the last few years I decided that it's time to head back to .NET world and see what's new. Actually, I never really left. There was a bunch of older .NET projects that I have maintained in the meantime and few new ones, but all of them were on full .NET Framework. My plan is to dive into .NET Core and ASP.NET Core. While I've been closely following all the new development around .NET Core, I'm yet to do a concrete project with it. Hopefully, this is about to change.

For start, I'm switching this blog to [Wyam](https://wyam.io/), a .NET Core based static site generator. [Hexo](https://hexo.io/) was one of the alternatives that I was looking into, but since it's Node.js based, I decided it's more appropriate to go with .NET Core based platform.

![Wyam](/images/2017-07-wyam.png)

It seems that each time when I try to return to blogging I switch the blog platform, so let's continue with that practice :)

## Phase 1 - Installing and initializing Wyam

Installation was easy as described in [Wyam documentation](https://wyam.io/docs/usage/obtaining). I have downloaded the latest  Windows Installer and run it. After that it's necessary to go to `%LocalAppData%\Wyam` and run `Wyam.Windows add-path` to add the Wyam installation folder to Windows PATH variable.

Next step, reading the documentation. Seriously, I do prefer to read the docs first to get myself more familiar with something I'm interested in and Wyam has a pretty good documentation.

My blog is hosted on GitHub Pages. Old version was using Jekyll. To start with the migration, I have created a new git branch. Initializing Wyam was as simple as `wyam new -r Blog` to create a new configuration using Blog recipe.

Wyam has created `config.wyam` file that can be modified. This is my first configuration:

```
#recipe Blog

Settings[Keys.Host] = "blog.miroslavpopovic.com";
Settings[BlogKeys.IncludeDateInPostPath] = true;
Settings[BlogKeys.RssPath] = "feed.xml";
Settings[BlogKeys.Title] = "Miroslav Popovic";
Settings[BlogKeys.Description] = "Full-stack .NET and JavaScript software architect";
```

Few things that are changed from the default. I prefer to have date in URL, so `BlogKeys.IncludeDateInPostPath` is set to `true`. By default, Wyam generates two feed files, one for RSS - `feed.rss` and one for Atom - `feed.atom` format. My old setup had one RSS file - `feed.xml`. To prevent subscribers from making changes in their feed readers, `BlogKeys.RssPath` was set to `feed-xml`. Other settings should be self-expanatory.

With this it was possible to build the blog `wyam build` or build and watch for changes `wyam build --watch`. For previewing the result in browser `wyam preview` runs the integrated server on port 5080 by default.

## Phase 2 - Moving assets

Jekyll used assets relative to root folder, like static pages (`about.md`), `/images`, favicons, etc. Wyam uses `/input` as a root, so all the files need to be moved there.

## Phase 3 - Migrating posts

Wyam Blog recipe also supports markdown by default. Migrating posts to Wyam was as simple as moving them from Jekyll's `_posts` folder to Wyam's `input/posts` folder and changing few things in [FrontMatter](https://wyam.io/docs/concepts/metadata#front-matter).

FrontMatter is a bit of metadata at the top of the post which you can use to define title, description, tags, dates, or any other custom metadata. There are some differences between Jekyll and Wyam FrontMatter syntax. I.e. tags in Jekyll are defined separated with space, like `tags: tag1 tag2 tag3` and that will create a single tag in Wyam. For Wyam, you need to either define them with array syntax `tags: [tag1, tag2, tag3]` or split them to multiple lines:

```
tags:
  - tag1
  - tag2
  - tag3
```

Another difference is with redirects. Jekyll redirects are defined with `redirect_from: "/some-url/"` and Wyam supports this syntax: `RedirectFrom: /some-url/`. The fact that you can define multiple redirects using the same syntax as for tags made me very happy. This is especially usefull if you are doing several migrations, like I did (from FunnelWeb to Jekyll to Wyam):

```
RedirectFrom:
  - resurrection
  - 2012/06/10/resurrection
```

Since I don't have that many posts, I did all of these changes manually, but you could easily to search/replace in files.

## Phase 4 - Tuning up the theme

The default Clean Blog theme looks very good, so that's what I have used. Overriding the parts of layout is as simple as copying and modifying the partial views from Clean Blog theme source, like `_Scripts.cshtml` (for defining Google Analytics script), `_Head.cshtml` (for favicons and other meta tags), etc. Modifying CSS was also simple. All that is required is a new file for style overrides - `assets/css/override.css`.

My blog is using Disqus for comments. Adding Disqus is described on [Wyam docs](https://wyam.io/recipes/blog/themes/cleanblog). I was a bit concerned with preserving existing comments, but there are solutions for that too. One is described by Erik Onarheim in his [migrating to Wyam](https://erikonarheim.com/posts/using-wyam-blog#customizing-wyam-with-disqus) post and another one is to use [Disqus URL mapper](https://help.disqus.com/customer/portal/articles/912757-url-mapper).

## Phase 5 - Deployment

Finally, the time has come to deploy. There's a pretty good guide about setting up the continuous deployment on [Wyam docs](https://wyam.io/docs/deployment/appveyor) so I won't repeat it here.

One problem I had is with git branches. My previous setup with Jekyll had `master` and `gh-pages` branches. Unfortunately, having the code in `master` branch and output in `gh-pages` does not work for user and organization pages on GitHub and my blog code is on user page. At least that's what the documentation told me. It only allows serving from `master` so I reorganized my git repository a bit. "Source" code is in `source` branch and AppVeyor build copies the output to `master` branch.

## Finally

This blog is now generated using Wyam. At least until the next migration :)
