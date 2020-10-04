---
title: "Azure DNS Zone Powershell Scripts"
date: 2019-03-04
description: import from previous blog.
---
I made some Azure DNS Powershell scripts! Why? Because I had to migrate hundreds of records from one DNS provider to Azure. The previous DNS provider allowed duplicate CNAME vs A/TXT/MX records. It was a MESS. I wanted a way to import, test, and clear records repeatedly so that I could validate that no DNS settings would change on migration.

The **README** on the repo has more information. Feel free to reach out with questions.

Link: [AzureDnsTools](https://github.com/mikeruhl/AzureDnsTools)



