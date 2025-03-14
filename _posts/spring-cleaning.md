---
layout: post
title: Spring cleaning
subtitle: How I finally made my data less messy
tags:
  - organization
  - notes
  - tasks
---
So, I've been very busy last few days, because my files and configs and everything was all over the place... So here's my journey:

## Baby steps: Obsidian!

for anyone as messy as I am, [Obsidian](https://obsidian.md/) is a must have app. It took me way too long to realize it's absolutely perfect. Just markdown, folders, and decent UI, simple enough to just work. There is a ton of resources and plugins readily available, allowing you to just tweak your way and be done with it. Yes, I've been tweaking my arch install endlessly too.

## Blogging with [jekyll](https://jekyllrb.com/)

It was not without a fight. I have never done much with ruby, and there were some issues with versions, imports, and ACL config when running in docker, but eventually I found a way.

The first thing I did was to do my CV in jekyll to try it out. I made a Makefile to make my life a bit easier which looked something like this:
```makefile title:"Makefile"
JEKYLL_VERSION=3.8
PORT=4000
build:
	docker run --rm  -p${PORT}:4000  --volume="${PWD}:/srv/jekyll"   -it jekyll/jekyll:${JEKYLL_VERSION}   jekyll build
serve:
	docker run --rm  -p${PORT}:4000  --volume="${PWD}:/srv/jekyll"   -it jekyll/jekyll:${JEKYLL_VERSION}   jekyll serve
shell:
	docker run --rm  -p{PORT}:4000  --volume="jekyll-cv:/srv/jekyll" --volume="${PWD}:/srv/old"   -it jekyll/jekyll:${JEKYLL_VERSION}  sh 
```
nothing fancy, but it made my life a bit easier.

The CV itself is rather easy and it's just one-file-contains-all kinda philosophy, which now in retrospect feels a bit against the whole idea of using jekyll, but well, live and learn. 
The idea of using one file with everything slammed together comes from my past implementation of [first VanillaJS/HTML implementation](https://github.com/vstkl/cv) which was nothing more than a fun way to pass the time in a boring job back then. 

So eventually i got that working in docker, running on my laptop, since my current situation is inadvertly serverless-y, and then I saw everyone was hosting jekyll on github pages, which - again - in retrospect is obvious solution. So after a bit of tinkering and tweaking with cloudflare I somehow managed to deploy the jekyll blog which you are reading to my domain directly from my github. I didn't look too much into it, I am always suspicious and I prefer to always self-host, but non-crucial data like my rambling on this blog and CV? If you find a way to exploit *that*, kudos my friend.

So to sum it up, the solution was obvious and I am stupid. Hopefully this will help someone in the future.

Farewell, V
