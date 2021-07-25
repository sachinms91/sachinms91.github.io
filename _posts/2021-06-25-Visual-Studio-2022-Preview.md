---
title: Visual Studio 2022 will be a 64 bit application and how? 
author: Sachin M S
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/BlogImage.png"
date: 2021-06-25 18:20:00 +0330
categories: [Technology, Visual Studio 2022]
tags: [VS2022]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/BlogImage.png"
---

 ![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/BlogImage.png)

Microsoft has recently announced the Visual Studio 2022 preview version which promises to be faster, more lightweight, better scalability for the enterprise large scale solutions.
 One of the key highlights in Visual Studio 2022 is that the core devenv.exe process will be a 64-bit application. It will have much more advantages of getting a larger data set, using more CPU registers, and taking advantage of more than 4GB of memory. 
 Developers can build more complex solution without running out of memory; open larger-scale solutions without slowing down overall Visual Studio performance.
 
|![VS2019Versus2022](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/VS2019Versus2022.png)|
|:--:|
| Fig. 1 - devenv.exe process of VS 2019 vs VS 2022 preview |

Earlier versions Visual Studio (upto VS 2019) happened to be a 32-bit application, however few of internal components such as MSBuild.exe, Microsoft.ServiceHub.Controller.exe would work with the 64-bit process and expand to 64 bit as needed. 

|![DevEnv2019ProcessExplorer](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/DevEnv2019ProcessExplorer.png)|
|:--:|
| Fig. 2 - Process Explorer showing various 32/64 bit exe's running under devenv.exe |

One important point to remember is that Visual Studio can create and run 64-bit applications on 64-bit computers for a long time, but it remained a 32-bit application itself and it can access up to 4 GB of maximum memory.

The devenv.exe file installation location for VS 2019 community versus VS 2022 Community preview clearly highlights this:

```C:\Program Files\Microsoft Visual Studio\2022\Preview\Common7\IDE```

```C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE```

If we open any ASP.NET project in Visual Studio, we could always target the application platform to be 32 bit or 64 system.

|![PlatformTarget](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/VS2022Preview/PlatformTarget.png)|
|:--:|
| Fig. 3 - Target platform options available for 32 bit devenv.exe |

## Conclusion

1. A 32-bit operating system cannot take full advantage of 64 bit features hence Visual Studio 2022 is shipped as 64 bit application.
2. The architecture of Visual Studio 2022 will remain same as earlier versions, with only additional advantages of support of 64-bit for a 64-bit operating system.
3. 64 bit application enables faster performance while loading  complex solutions (with 100s of projects) without running out of memory.