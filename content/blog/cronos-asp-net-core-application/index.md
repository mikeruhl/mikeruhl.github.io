---
title: "Cronos - ASP.NET Core Application"
date: 2018-03-28
description: import from previous blog.
cagetories: [".NET Core"]
---
I wrote an asp.net core application. It's live at [https://cronos.frenetik.io](https://cronos.frenetik.io). It is an app that helps you create a chronological playlist based on an artist for Spotify. The source is up at [https://github.com/mikeruhl/cronos](https://github.com/mikeruhl/cronos). I won't go into much detail here since the readme covers a lot on github.

Just some backstory: A friend had posted a request on facebook that Spotify should offer this ability. I figured it would be a fun project so I started working on it in spare time. 1 month later, I had a working application. The process went very smooth due to a library I found at [https://github.com/dotnetfan/FluentSpotifyApi](https://github.com/dotnetfan/FluentSpotifyApi). It's very well written and I really appreciate the work that went into it. I had started futzing around with a proof of concept using RestSharp when I figured someone else had already done the dirty work. Sure enough, this great library fell into my lap after a quick google search.

You'll see from the source, I put some boilerplate session handling in `CronosBaseController.cs`. I liked the way that turned out, even though I didn't use it for any other controllers. I'm getting into the habit of hiding code that won't change and is on a different scope from the rest. I found it easier to work in `HomeController.cs` without that session code.

The code could use some refactoring. It also needs tests. I released it in a beta sense, and based on the fanfare (avg 1 user per day) I can guess it's not going to get much use. So I'll leave it where it stands and move on to the next project.



