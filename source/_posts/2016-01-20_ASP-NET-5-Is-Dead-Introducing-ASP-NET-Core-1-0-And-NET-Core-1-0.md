---
title: ASP.NET 5 已死 隆重介绍 ASP.NET Core 1.0 和 .NET Core 1.0
categories:
- .NET
- ASP.NET
tags:
- ASP.NET
- ASP.NET 5
- ASP.NET Core
- NET Core
date: 2016-01-20 23:43:30
---
# 缘由

  晚上回来就看到有博文说`ASP.NET 5`已死,其来源出自于[Scott Hanselman][2]的博客，下面是原文。

# 个人观点：

  >1. 命名：由于现在`asp.net`已开源，并支持跨平台,这是一种新的实现，而且和`asp.net 4.6`是并行关系，不是在4.6的基础上升级，所以不应该沿用之前的命名。

  >2. 已死：由于`asp.net 5`是一种新的实现，不是原来版本的升级，已重命名，所以说，`asp.net 5`算是死了。不过，还是有些人习惯叫`asp.net 5`。

# 原文

** Naming is hard. **

  >There are only two hard things in Computer Science: cache invalidation and naming things. - Phil Karlton

  It's very easy to armchair quarterback and say that "they should have named it Foo and it would be easy" but very often there's many players involved in naming things. ASP.NET is a good 'brand' that's been around for 15 years or so. ASP.NET 4.6 is a supported and released product that you can get and use now from [http://get.asp.net](http://get.asp.net).

  However, naming the new, completely written from scratch ASP.NET framework "ASP.NET 5" was a bad idea for a one major reason: 5 > 4.6 makes it seem like ASP.NET 5 is bigger, better, and replaces ASP.NET 4.6. Not so.

  So we're changing the name and picking a better version number.

** REINTRODUCING ASP.NET CORE 1.0 AND .NET CORE 1.0 **

  * ASP.NET 5 is now ASP.NET Core 1.0.

  * .NET Core 5 is now .NET Core 1.0.

  * Entity Framework 7 is now Entity Framework Core 1.0 or EF Core 1.0 colloquially.

  Why 1.0? Because these are new. The whole .NET Core concept is new. The [.NET Core 1.0 CLI][0] is very new. Not only that, but .NET Core isn't as complete as the full .NET Framework 4.6. We're still exploring server-side graphics libraries. We're still exploring gaps between ASP.NET 4.6 and ASP.NET Core 1.0.

  ![][1]

** WHICH TO CHOOSE? **

  To be clear, ASP.NET 4.6 is the more mature platform. It's battle-tested and released and available today. ASP.NET Core 1.0 is a 1.0 release that includes Web API and MVC but doesn't yet have SignalR or Web Pages. It doesn't yet support VB or F#. It will have these subsystems some day but not today.

  We don't want anyone to think that ASP.NET Core 1.0 is the finish line. It's a new beginning and a fork in the road, but ASP.NET 4.6 continues on, released and fully supported. There's lots of great stuff coming, stay tuned!

---

# 译文

** 起名真难 **

>计算机科学中只有两件难事：缓存失效和命名。——Phil Karlton

  “他们就该给它起个名字叫Foo，多简单的事” 纸上谈兵说说很容易，但是起名字这件事经常牵扯到很多因素。ASP.NET 作为一个好“牌子”已经有15年了。ASP.NET 4.6是一个受支持的已发布产品，你可以在 [https://get.asp.net](https://get.asp.net) 获取。

  然而，把一个全新的、完全重写的ASP.NET框架命名为 “ASP.NET 5” 不是一个好主意，一个主要原因就是：5 > 4.6 让人觉得 ASP.NET 5 更大、更好，是取代ASP.NET 4.6的。并不是。

  所以我们重新命名并选了一个更好的版本号。

** 隆重介绍 ASP.NET Core 1.0 和 .NET Core 1.0 **

  * ASP.NET 5 现在叫做 ASP.NET Core 1.0
  * .NET Core 现在叫做 .NET Core 1.0
  * Entity Framework 7 现在叫做 Entity Framework Core 1.0 或者简称 EF Core 1.0

  为什么选1.0？因为它们是全新的。整个.NET Core概念就是全新的。.NET Core CLI 是非常新的东西。（译注：.Net Core Command Line Interface ，将取代DNX）

  不仅如此，.NET Core还不像.NET Framework 4.6那样完整。我们仍在完善服务端图形库(server-side grahpics libraries)，我们仍在填补ASP.NET Core 1.0和ASP.NET 4.6之间的缺口。

    ![][1]

** 如何选择？ **

  明确一下，ASP.NET 4.6是更成熟的平台。是经过实战（battle-tested）的目前已发布的可以用版本。

  ASP.NET Core 1.0则是1.0版本，包括了Web API和MVC，但不包括SinglR和Web Pages。目前还不支持VB和F#。这些都会在将来实现，但目前还没有。

  我们不想让人认为ASP.NET Core 1.0是个终点线，它是一个新的起点和新的分支。

  ASP.NET 4.6将继续前行，发布并全面受到支持。别走开，更多精彩内容即将呈现。


FROM:[Scott Hanselman Blog][2]

[2]:http://www.hanselman.com/blog/ASPNET5IsDeadIntroducingASPNETCore10AndNETCore10.aspx
[1]:http://www.hanselman.com/blog/content/binary/Windows-Live-Writer/Reintroducing-ASP.NET-Core-1.0-and-.NE.0_B840/image_0e978596-bd85-42ed-8d27-c16e119bca5d.png
[0]:http://www.hanselman.com/blog/ExploringTheNewNETDotnetCommandLineInterfaceCLI.aspx
