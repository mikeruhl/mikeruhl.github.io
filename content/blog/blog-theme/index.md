---
title: "Blog Theme Update"
date: 2017-10-09
description: import from previous blog.
cagetories: ["docker", "ghost", "nginx", "site news"]
---
I've moved from the default theme. I was using it even with the old site. I found a really sleek theme called [StayPuft](https://github.com/dlecina/StayPuft). It just looks like the author hasn't updated it for Ghost v1 yet. I forked the repo, which is available [here](https://github.com/mikeruhl/StayPuft_frenetik). If you're having trouble with StayPuft, perhaps give my fork a try. Keep in mind it has a different color scheme.

There were a few technical issues I had to overcome with this theme. They were quick to resolve and I had a good time doing it.

### max_body_size in nginx.conf

I hadn't set this. I was trying to upload this theme but the size is too big (2mb). So, I had to update nginx.conf's http section and include `client_max_body_size 2m;`. The default is 1mb. This file is located in /etc/nginx. I am running nginx in a docker container so I just had to edit the file in my docker volume and restart nginx. It was super-simple.

### obsolete helpers in Ghost

The main reason I had to fork the theme was because it was written for v.11. In v1 the ghost team changed some helpers involving images. The absolutely awesome part about it is that when you upload a theme, ghost tells you all the parsing errors in a great format that's easy to debug and fix. I am so very impressed with ghost's features.

In closing, I'll be tweaking this theme as I go. I don't like where the search results are for ghostHunter. I want to add some features and adjust the colors as well. The [repository](https://github.com/mikeruhl/StayPuft_frenetik) will stay current!



