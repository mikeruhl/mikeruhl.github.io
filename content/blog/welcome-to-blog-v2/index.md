---
title: "Welcome to blog v2!"
date: 2017-10-08
description: import from previous blog.
cagetories: ["first", "personal", "docker"]
---
I committed the cardinal sin of devops: upgrading without backing up. It was quite unfortunate. Sometimes I think, "it's just my site, who cares," but I lost a few good hours of explaining something really cool.

To be fair, this is the first time it's happened for real. In prior iterations, I've backed up my database and restored it. This time I figured since the database was persisted on the filesystem, it would just start back up ok. Upon closer inspection, it appears my ghost installation, at some point, reverted to a vanilla install and started using the sqlite local database again. I'm not exactly sure how, but it started back up from scratch, so that .db file was brand new when I finally inspected it. Half my posts were in that while half were in a mariadb database. I have the mariadb posts. I don't have the sqlite posts. Those, I suspect, are gone. So, backup and backup some more. Thinking "well, my data is persisted" didn't cut it. An updated image started up and cut that theory down pretty quickly.

**The good news!** Yes, there's good news! I have updated containers running. I _sincerely hope_ I've learned my lesson and will read release notes before `docker pull`ing any new containers. I'll re-post my configuration with updated settings. It's worth reviewing. A few things changed since updating. For the record, I've updated all containers along with the docker engine. So pretty neat. And I've added a few perks. This new version of Ghost is pretty snazzy so I don't regret much.

I might have to invest in a dev environment, even for this dinky site. Making changes directly in production is never a good idea without testing it first. Docker makes it easy, too. I should post a set up of that. More to come...



