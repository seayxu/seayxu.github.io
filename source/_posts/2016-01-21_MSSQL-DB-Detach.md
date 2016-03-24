---
title: MS SQL Server 数据库分离--SQL语句
categories:
- Database
- MSSQL
tags:
- Database
- MSSQL
- 数据库
date: 2016-01-21 17:31:30
---

# 前言

今天在在清理数据库，是`MS SQL Server`,其中用到分离数据库文件。在这过程中，出现了一个小小的问题：误将数据库日志文件删除了，然后数据就打不开了，除了脱机，其他操作都报错。

----------

# 数据库分离

## 常规方法

此方法是常规惯用的方式，多步骤。

如图所示：

![图一][1]

![图二][2]

----------

## 粗暴方法

此方法简单粗暴，非常实用，一条`SQL`语句就搞定了。

SQL语句实现： `EXEC sp_detach_db [DatabaseName]`

示例：`EXEC sp_detach_db OA`

  [1]: http://segmentfault.com/img/bVsoMZ
  [2]: http://segmentfault.com/img/bVsoM0
