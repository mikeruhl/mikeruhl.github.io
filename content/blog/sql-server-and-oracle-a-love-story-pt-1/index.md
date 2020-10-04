---
title: "Sql Server and Oracle: A Love Story Pt 1"
date: 2017-10-10
description: import from previous blog.
cagetories: ["oracle", "sql server", "migration", "database"]
---
I was given the most honorable task of migrating a fairly large SQL Server database over to Oracle 12c at my day job. In doing so, I have gleened a ton of knowledge about why you should never do this. It's a tough line: future proofing your app versus using proprietary tech for one platform that may not transfer over to another platform. We have a good mix of the latter.

I have found one particular great thing out today. Oracle's Sql Developer has a fairly rudimentary migration feature for moving Sql Server and Sybase databases over to their platform. The trick to grab the ddl straight from the source database is to import it. This can be done by downloading a jdbc driver and telling Sql Developer about it [link](https://oracle-base.com/articles/misc/sqlserver-connections-in-sql-developer).

What I ran into today was having an instance on a server. In order to validate scripts and get things moving, I set up an identical Sql Server on my dev machine with the same schema as the one I'm trying to migrate. As I found with an instance, there was no where to put it in the box:


![newdb](/content/images/2017/10/newdb.jpg)

Hostname is JUST for the server name. If you have an instance name, you're out of luck. So I started thinking about the connection string this form is no doubt generating with these boxes. Eureka! You can _inject_ the instance into the connection string by appending it to the port. So in your port, just add **1433;instance=sqlserver**. That appends the connection string and you can now connnect!

Once the Sql Server connection is made, you can right click on it and select 'Migrate Database.' From there, you'll learn as I did that that tool is nothing short of a pain in the rear.



