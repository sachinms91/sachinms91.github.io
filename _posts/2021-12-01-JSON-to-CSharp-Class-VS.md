---
title: Converting JSON object to C# class 
author: Sachin M S
description: Global Using is a new feature introduced with C# 10.0 to eliminate multiple  import statemtns in class files
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/globalusings-in-csharp10.png"
date: 2021-12-01 01:00:00 +0330
categories: [Technology, Visual Studio]
tags: [Visual Studio Tips]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/globalusings-in-csharp10.png"
---

![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/globalusings-in-csharp10.png)

Every C# class file begins with a list of ```using``` statements that are necessary for implementation. Much of this code is repetitive and takes up more bytes in files.

If we create an ASP NET Core Web Application(MVC) with Visual Studio 2022 preview or higher with .NET 6 SDK we will be getting the below code in ```HomeController.cs```



As you can see from above that most of these namespaces imported here are likely to be required in other .cs files as well. The developer will end up writing multiple imports of the same namespace in multiple .cs files. To Avoid this with C# 10.0 Microsoft introduced the concept of declaring and importing namespaces globally.

## Adding Global 'Using.cs' file to a project in .NET 6
Add a new file called ```Using.cs``` (can be added to the project root level. The name of the file can be anything) and start importing most likely used namespaces in this file by prefixing with  ```global``` keyword. 


The content of ```Using.cs``` will be:

```cs
global using GlobalUsingsDemoApp.Models;
global using Microsoft.AspNetCore.Mvc;
global using Microsoft.Extensions.Logging;
global using System;
global using System.Collections.Generic;
global using System.Diagnostics;
global using System.Linq;
global using System.Threading.Tasks;
```

That's it! Now your ```HomeController.cs``` can be simplified  and it can start referring classes defined namespaces present in ```Using.cs```

```cs
namespace GlobalUsingsDemoApp.Controllers
{
    public class HomeController : Controller
    {
        private readonly ILogger<HomeController> _logger;

        public HomeController(ILogger<HomeController> logger)
        {
            _logger = logger;
        }

        public IActionResult Index()
        {
            return View();
        }

        public IActionResult Privacy()
        {
            return View();
        }

        [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, NoStore = true)]
        public IActionResult Error()
        {
            return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
        }
    }
}
```
## Combining Top-level statements(.NET 5) with global using in C#

Top-level statements enable developers to avoid the extra ceremony required by placing the program's entry point in a static method in a class. The typical starting point for a new console application looks like the following code:



