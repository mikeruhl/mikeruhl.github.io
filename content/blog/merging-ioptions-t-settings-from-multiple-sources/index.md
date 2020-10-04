---
title: "Merging IOptions<T> settings from multiple sources"
date: 2017-11-26
description: import from previous blog.
cagetories: [".NET Core", "Configuration", "DevOps", "Web"]
---
.NET Core rocks for so many reasons. One thing I've been using recently is demoing updates and real-world debugging via Azure and then deploying to my VPS in a Docker container somewhere else. I don't generate enough traffic to make an Azure web service more affordable than a VPS, which is why I don't run everything from the cloud. So, QA is a WebApp running on Azure in a cheap tier, which I use my credits from my MSDN subscription for, then my production is in Docker running from the same box as this blog.

.NET Core makes configuration between these two sources so simple. If you know how to use environment variables in docker, in an OS, and in a cloud service (like Azure), then you can deploy any of those ways without changing anything at build or run time (aside from initial set-up).

Here's the options class I'm dealing with:

```csharp
ublic class EmailSettings
{
    public string MailGunApiKey { get; set; }
    public string ApiBaseUri { get; set; }
    public string From { get; set; }
    public string Domain { get; set; }
    public string RecaptchaApiKey { get; set; }
    
    public bool IsValid()
    {
        return !string.IsNullOrEmpty(MailGunApiKey) &&
            !string.IsNullOrEmpty(ApiBaseUri) &&
            !string.IsNullOrEmpty(From) &&
            !string.IsNullOrEmpty(Domain) &&
            !string.IsNullOrEmpty(RecaptchaApiKey);
    }
}
```

Super simple, I have a form on a web page to email me. I implemented ReCaptcha v2 to cut down on spam and I use the MailGun API to send the email. `ApiBaseUri` is the base API URL for MailGun, `From` is the email I'm sending to (me), `Domain` is the domain I'm sending from, and the two ApiKey properties are for each API, respectively.

The hurdle I had to jump across yesterday dealt with [IOptions<T>](https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.options.ioptions-1?view=aspnetcore-2.0). Typically, you can easily deserialize an object from json into your settings object with a one-liner. Then you can use Dependency Injection to access it in a controller. Here's an example:

[//Startup.cs](//Startup.cs)

```csharp
ublic void ConfigureServices(IServiceCollection services)
    {
        services.Configure<EmailSettings>(Configuration.GetSection("EmailSettings"));
    }
```

This works great when all of your properties in that Options class are in one location with equal security requirements. As you can see, I created a class, though, where some properties could be stored in a file and others (like the private api keys) needed to be stored as environment variables, to avoid being committed to source. What I wanted was the portability and ease to store many config variables in a file with the security of keeping some out of source and directly on the host.

So, I came up with a solution of blending sources into one class so that they would be available as one. In order to load my api keys separately, this is what I added in place of the statement noted above:

```csharp
ublic void ConfigureServices(IServiceCollection services)
{
//...
    services.Configure<EmailSettings>(options=> {

        options.ApiBaseUri = Configuration["EmailSettings:ApiBaseUri"];
        options.From = Configuration["EmailSettings:From"];
        options.Domain = Configuration["EmailSettings:Domain"];
        options.MailGunApiKey = Configuration["EmailSettings:MailGunApiKey"];
        options.RecaptchaApiKey = Configuration["EmailSettings:RecaptchaApiKey"];
        if (string.IsNullOrEmpty(options.MailGunApiKey) &&  Configuration.GetValue<string>("MAILGUN_API_KEY") != null)
        {
            options.MailGunApiKey = Configuration.GetValue<string>("MAILGUN_API_KEY");
        }
        if (string.IsNullOrEmpty(options.RecaptchaApiKey) && Configuration.GetValue<string>("RECAPTCHA_API_KEY") != null)
        {
            options.RecaptchaApiKey = Configuration.GetValue<string>("RECAPTCHA_API_KEY");
        }

    });
    //...
}
```

From this I'm getting exactly what I want from each "source". If I want to set variables in my file, I can and they will populate and not be overwritten by environment variables. Otherwise, it checks for environment variables too. I listed out all of these properties to show that you can also mix and match what you grab from JSON on a per-property level.

To finish this up, I call the EmailSetting.IsValid() method in my page generation to decide whether to build the html for the email form if one of these things is missing. That way, I won't have unnecessary broken calls to my API and it's also a quick way to see if something is missing. Combining this method in production with UserSecrets in Development is an excellent way to manage your dev and prod configs separately and securely.

More info on Configuration in .NET Core 2 can be found [here](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration?tabs=basicconfiguration).



