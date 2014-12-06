---
layout: page
sidebar_name: Github projects
title: Github projects
sort: 2
---

### [Finger Trees](https://github.com/cantsin/fsharp-finger-trees)

[F#](http://fsharp.org/) has interested me for many years, so I figured it was finally time to bite the bullet and properly learn the language.

The data structure I chose to implement was a finger tree: a data structure with first-order nested types using monoids and reductions (via generics/parametric polymorphism). The reference paper is [Finger trees - a simple general-purpose data structure (Hinze, Paterson)](https://github.com/cantsin/fsharp-finger-trees/blob/master/reference/Finger%20trees%20-%20a%20simple%20general-purpose%20data%20structure%20(Hinze,%20Paterson).pdf?raw=true). As a bonus, I also wanted to test C# interoperability with F# code.

I wrote this while learning F#, so I am afraid the code is not quite idiomatic. Nonetheless, I am very impressed with the language so far. See [this blog post](/2014/11/30/fsharp/) for more observations.

As of November 22, 2014, the project is complete, although I may return to it some day to add laziness. Currently the code is not optimized at all.

### [PCGen Rules](https://github.com/gamelost/pcgen-rules)

I have been consistently frustrated with the (sad) state of affairs with [PCGen](http://pcgen.sourceforge.net/01_overview.php), an open source character generator for role-playing games. So I decided to write a Haskell program to parse the rule sets it uses, in the hopes that I would be able to build a better platform for myself and my gaming friends. Of course, this turned out to be a far bigger project than I anticipated.

Currently the code consists of a whole lot of monadic parsers. I'm not yet quite sure where all this will end -- but I'm already thinking about ways to write a better rule based inference engine. Maybe something on top of [MiniKanren](http://minikanren.org/).

As of {{ site.time | date: '%B %d, %Y' }}, this is still a work in progress.

### Git Tracker

This project is currently in its planning stages. I want a better way to track my programming, writing, and research habits. Since I (ab)use git, and have both private and public repositories scattered everywhere, I figured that I would jump on the [Quantified Self](http://quantifiedself.com/) bandwagon and make my own habit tracker.

Currently, I have wireframes on [Balsamiq](https://balsamiq.com/) and I have settled on several graphical representations for data: [heat](http://en.wikipedia.org/wiki/Heat_map) and [tree maps](http://en.wikipedia.org/wiki/Treemapping).

### More

All of my [public repositories](https://github.com/cantsin?tab=repositories) are on github.
