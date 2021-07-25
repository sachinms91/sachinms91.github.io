---
title: Global Using in C# 10
author: Sachin M S
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/GlobalUsings/globalusings-in-csharp10.png"
date: 2021-07-25 20:00:00 +0330
categories: [Technology, C#10]
tags: [C# 10 Global Using]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/GlobalUsings/globalusings-in-csharp10.png"
---

![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/GlobalUsings/globalusings-in-csharp10.png)

Every C# class file begins with a list of ```using``` statements that are necessary for implementation. Much of this code is repetitive and takes up more bytes in files.

If we create an ASP NET Core Web Application(MVC) with Visual Studio 2022 preview or higher with .NET 6 SDK we will be getting the below code in ```HomeController.cs```

```cs
using GlobalUsingsDemoApp.Models;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Threading.Tasks;

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

As you can see from above that most of these namespaces imported here are likely to be required in other .cs files as well. The developer will end up writing multiple imports of the same namespace in multiple .cs files. To Avoid this with C# 10.0 Microsoft introduced the concept of declaring and importing namespaces globally.

## Adding Global 'Using.cs' file to a project in .NET 6
Add a new file called ```Using.cs``` (can be added to the project root level. The name of the file can be anything) and start importing most likely used namespaces in this file by prefixing with  ````global``` keyword. 

![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/GlobalUsings/usings-in-vs2022.PNG)

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

```cs
using System;

namespace Application
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
Above 11 lines contain only one line of executable code ```Console.WriteLine("Hello World!");```. You can simplify that program with the new top-level statements feature. That enables  to remove all but two of the lines in this program:

```cs
using System;
Console.WriteLine(args);
```
We need not declare  ```args``` variable. For the single source file that contains your top-level statements, the compiler recognizes args to mean the command-line arguments. The type of args is a string[], as in all C# programs.

With global using C# 10.0 feature, the console app code can be reduced to 1 line!
```cs
Console.WriteLine(args);
```

## Conclusion
With global using C# 10.0 feature Microsoft has reduced overhead of importing namepsaces and when combined with other .NET features such as Top-level statements, they simplify a lot of things for developers.



