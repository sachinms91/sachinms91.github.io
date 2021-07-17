---
title: Build a Minimal API in .NET 6
author: Sachin M S
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/BlogPostHeader.jpg"
date: 2021-07-17 20:15:00 +0330
categories: [Technology, .NET 6]
tags: [.NET 6 Minimal API]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/BlogPostHeader.jpg"
---

 ![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/BlogPostHeader.png)

## Background

Building lightweight APIs in ASP\. NET Core was not possible until .NET 6. Developers were confined to use the MVC pattern of Web API's which was a bit overwhelming for beginners.

The conventional ASP\. NET Core API's/Web projects involved lot of ceremonies associated with them:

1. ```Program.cs``` file will have ```Main``` method calling ```CreateHostBuilder``` method.
2. ```CreateHostBuilder``` will call ```CreateDefaultBuilder``` method which configures bunch of defaults such as logging, configuration in a specific order.
3. ```ConfigureWebHostDefaults``` will be invoked to use ```Startup.cs``` file. 
4. ```Startup.cs``` has ```Configure``` and ```ConfigureServices``` methods to configure HTTP request pipeline and handle Dependency Injection(DI).

 |![Fig1](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/Cermonies.PNG)|
 |:--:|
 | Fig. 1 - Ceremonies involved in a conventional ASP\.NET Core APIs|
Imagine if a novice developer is trying to understand the above bits of defaults whose intention is to quickly build an API endpoint! Sounds too complicated, isn't it?

## What is a Minimal API?

The idea of Minimal API is to let developers start with simple APIs (i.e. fewer ceremonies) and then start building on top of it. This is really helpful for developers who are new to the ASP\. NET Core ecosystem.
Minimal API's also help to build  smaller microservices-based API's 

## Creating a Minimal API  project in .NET 6

Open windows terminal/command prompt from any folder and type the below command and open the folder in Visual Studio. Please ensure you have at least .NET 6 preview 6 SDK version installed for this to work.

```csharp
dotnet new web -o MinApi
```
 |![Fig2](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/MinApiProject.PNG)|
 |:--:|
 | Fig. 2 - MinApi project template scaffolding in Visual Studio 2022 Preview |

That's it! You have your first minimal API ready. Whatever goes into the lambda function (2nd parameter to MapGet method) below acts as an API endpoint.  

```csharp
app.MapGet("/", () => "Hello World!");
```

To see the real benefits of minimal API examine carefully how we can simplify an MVC scaffolded API controller, please refer to the below screenshot: 

Each of the HTTP verbs get mapped to ```app.Map<HttpVerb>()``` methods in minimal API.

 |![Fig3](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/ApiControllerVersusMinimalApi.PNG)|
 |:--:|
 | Fig. 3 - API methods of a conventional APiController versus Minimal API|

It is evident from above that developers can now write APIs in ASP\. NET Core with fewer lines of code in a simpler way! Having said that, minimal APIs doesnt take away any of .NET Core features. All it does is to reduce API boilerplate code. 
## How Dependency Injection works with Minimal API?
Let us say if we want to offload the logic of the API endpoint to a separate file or a service rather than writing inside a lambda function. This can be achieved by importing ```Microsoft.Extensions.DependencyInjection``` namespace. The below example shows how to invoke a service method inside ```app.MapGet``` method. 
 
 ```ToDoService.cs``` file: 
 ```cs
 namespace MinApi.ToDoService
{
    public interface IToDoService
    {
        string GetTask(int id);
    }
    public class ToDoService : IToDoService
    {
        public string GetTask(int id)
        {
            return $"Task # {id.ToString()}";
        }
    }
}
 ```
 
 ```Program.cs``` file:
 ```csharp
 using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using MinApi.ToDoService;

var builder = WebApplication.CreateBuilder(args);
builder.Services.AddSingleton<IToDoService, ToDoService>();   

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}

app.MapGet("/GetTask/{id}", (HttpContext context, ToDoService todoService, int id) => {
    context.Response.WriteAsync(todoService.GetTask(id));
    });

app.Run();
 ```
For more information on Minimal API please refer to the below video from David Fowler, Damian Edwards, Stephen Halter and Jon Galloway showcased in **ASP\. NET Community Standup - Minimal APIs**

[![ASPNETCommunityStandUpVideo](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/MinimalAPI/YTVideoThumbnail.jpg )](https://www.youtube.com/watch?v=enAskgcF0c0) 