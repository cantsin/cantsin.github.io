---
layout: post
title: git-tracker, Take Two
date: 2015-01-09
---

> Men have become the tools of their tools.

> Henry David Thoreau

[git-tracker](https://github.com/cantsin/git-tracker) is now good enough for daily use, so I have marked it as v1.0 accordingly. Only two graphs are used to visualize git activity: a [heat map](http://en.wikipedia.org/wiki/Heat_map) and a [tree map](http://en.wikipedia.org/wiki/Treemapping) (the latter in conjunction with tags).

To use `git-tracker` effectively, it is recommended to use a machine ssh key (e.g., a ssh key that is not pass-phrase protected and has read-only access to your repositories). I did not want to store ssh pass-phrases, as that is a big security risk, so this is the next best thing.

Even though functionality is fairly limited, I have been using it every day and it is already better than my previous git monitoring tool. Part of this is because I pared away all the extraneous stuff that was not needed. But really, it turns out that what I really cared about was tracking relatively recent git activity (such as in the last three months).

<!--more-->

## The Ingredients

This project was an easy one, since I used a few open source components that I was already familiar with.

For the backend, I used the excellent python micro-framework [Flask](http://flask.pocoo.org/) with [SQLAlchemy](http://www.sqlalchemy.org/). Low-level git access is done via [pygit2](https://github.com/libgit2/pygit2).

The frontend is plain ES6 javascript, with some [RxJS](https://github.com/Reactive-Extensions/RxJS) thrown in. For the heat map, I used [cal-heatmap](https://github.com/kamisama/cal-heatmap). Nothing too complicated, but the frontend is not as interactive as I would like it to be.

Which leads me to...

## git-tracker v2.0

There is still plenty left to do; `git-tracker` is by no means 'done.'

Some features for v2.0:

- Quantify PR activity across your projects.
- Better date range handling.
- A more versatile frontend (I want to try out [Elm](http://elm-lang.org/)).
- Docker support to make `git-tracker` instances easier to deploy/maintain.
- In conjunction with the above, a cron job to automate updating repositories.
- Custom heat-maps (I'm not entirely satisfied with `cal-heatmap`)

## Lessons Learned

At the beginning of this project, I prototyped a lot of git tracking ideas with [Balsamiq](https://balsamiq.com/) which turned out to be a good decision. I was able to cut away a lot of unnecessary features. That being said, there were a couple of features I did not anticipate, such as the need to add email accounts in order to comprehensively identify your git commit activity. (I commit code under two email aliases.) I did not round trip back to Balsamiq for these new features, though in hindsight I should have.

I chose to focus on the speed of development by using familiar tools, and altogether `git-tracker` v1.0 took me very little time -- perhaps a few days of development work altogether. For the next version, I want to add in something more challenging. I briefly considered using rust (now in [v1.0 alpha](http://blog.rust-lang.org/2015/01/09/Rust-1.0-alpha.html)!) but I do not think it is the proper fit for `git-tracker`. (That being said, I am using rust in other projects.) More likely, I will write an [Elm](http://elm-lang.org/) component for a better heat map implementation. (The nice thing about Elm is that you can embed it directly into a `<div>`.)

It does help to quantify git activity across different categories: I can see that I do most of my writing on weekends, for example. The last three months have been fairly productive (with some 'holes' in certain projects, of course.) Unfortunately my research notes have been sparsely updated lately, so there is still room for improvement, though!
