---
title: Converting JSON object to C# class in Visual Studio
author: Sachin M S
description: Simple and easy way to convert a JSON object to C sharp class
header-img: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/globalusings-in-csharp10.png"
date: 2021-12-20 01:00:00 +0330
categories: [Technology, Visual Studio 2022]
tags: [VS Tips and Tricks]
image: "https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/globalusings-in-csharp10.png"
---
![BlogImage](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/PasteSpecial.png)
 Fig. 1 - Visual Studio option tp 'Paste JSON as Class'


JSON stands for Javascript Object Notation used for storing and transferring data. Converting a JSON object to C# class type is one of the common scenarios in cases where both sender and receiver agree upon a predefined set of message contracts. Especially in an event-driven messaging architecture system (such as Azure Service Bus, Rabbit MQ, etc.)

The benefits of having to read a C# class object rather than reading JSON object properties is that it eliminates any typos and provides compile-time errors(if any)

There are quite a few websites that allow converting a JSON object to C# class object e.g: https://json2csharp.com/, https://www.site24x7.com/tools/json-to-csharp.html, etc. Some of these sites might store your inputs in their servers(you never know). It is not safe to use if you input a JSON object that is part of your company/client data.

VS Studio out of the box provides this feature if the *ASP.NET and Web Development* workload is installed during Visual Studio installation. Here is how to use it: 

1. Create a new class file (.cs for C#) and remove all pre-defined code inside ( Right-click on project -> Add -> Class)
2. Copy JSON data to clipboard 
3. Open the .cs file and navigate to Edit -> Paste Special -> Paste JSON as Class 

```json
{
Employees: [{
  "id": 1,
  "first_name": "Jean",
  "last_name": "Penn",
  "email": "jeanenn@abc.org",
  "gender": "Female",
  "ip_address": "26.55.193.2"
}, {
  "id": 2,
  "first_name": "Giovani",
  "last_name": "Fred",
  "email": "gfred1@abc.ord",
  "gender": "Male",
  "ip_address": "209.109.4.212"
}, {
  "id": 3,
  "first_name": "Ed",
  "last_name": "Boyce",
  "email": "edboyce@abc.org",
  "gender": "Female",
  "ip_address": "192.66.142.244"
}, {
  "id": 4,
  "first_name": "Will",
  "last_name": "Smith",
  "email": "wsmith3@abc.org",
  "gender": "Male",
  "ip_address": "96.66.148.14"
}]
}
```

```csharp
public class EmployeeList
    {
        public Employee[] Employees { get; set; }
    }

    public class Employee
    {
        public int id { get; set; }
        public string first_name { get; set; }
        public string last_name { get; set; }
        public string email { get; set; }
        public string gender { get; set; }
        public string ip_address { get; set; }
    }
```
Note: Make sure that the JSON copied to the clipboard is valid and well-formatted(Use Notepad++ for this) else VS will throw an error as shown below:

![Fig2](https://cdn.jsdelivr.net/gh/sachinms91/blog-images/images/JSON2CSharp/PasteSpecialError.png)
 Fig. 2 - Visual Studio error in case of invalid JSON being pasted using 'Paste Special'


Hope this information is useful next time when you need it!