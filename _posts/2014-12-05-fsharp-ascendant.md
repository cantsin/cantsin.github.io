---
layout: post
title: F# Ascendant
comments: true
date: 2014-12-05
---

> [His name](http://en.wikipedia.org/wiki/Alaric_I) is indeed branded with the reproachful epithets of pirate and robber, to which the conquerors of every age are so justly entitled...

> [Edward Gibbon, The Decline and Fall of the Roman Empire](http://www.gutenberg.org/files/25717/25717-h/25717-h.htm)

These days, it seems like [F#](http://fsharp.org/) is [ascendant](http://www.infoworld.com/article/2610183/microsoft-net/article.html).

I have long considered [OCaml](https://ocaml.org/) one of the nicer languages I have worked with, though I have sadly not touched it in years. So when I had the opportunity and time for some exploratory research, I jumped at the chance to try out F#. The world needs more [ML](http://en.wikipedia.org/wiki/ML_(programming_language)) dialects!

Coding in F# was very comfortable, much like slipping into a warm bath. But I suspect the intervening years, and particularly deep explorations into [Haskell](https://www.haskell.org/haskellwiki/Haskell), have changed my programming language expectations in ways I did not anticipate at first.

But let's talk about my first F# project for a bit.

<!--more-->

## Finger Trees

I chose to implement the [finger trees](http://en.wikipedia.org/wiki/Finger_tree) data structure because I wanted to play around with F#'s typing system. Finger trees in particular require first-order nested types: at depth 1, `Node<T>`, at depth 2, `Node<Node<T>>` and so on. Furthermore, `Node`s are parameterized by [monoids](http://mathworld.wolfram.com/Monoid.html), and thanks to some clever use of monoidic properties, this allows the finger tree to operate as a generic data structure.

As per the [original paper](https://github.com/cantsin/fsharp-finger-trees/blob/master/reference/Finger%20trees%20-%20a%20simple%20general-purpose%20data%20structure%20(Hinze,%20Paterson).pdf?raw=true), I implemented:

- a random access list
- a priority queue
- an ordered sequence
- and an interval tree.

All this code is on my [Github repository](https://github.com/cantsin/fsharp-finger-trees).

(For a more practical implementation of finger trees, see Haskell's [Data.Sequence](https://hackage.haskell.org/package/containers-0.3.0.0/docs/Data-Sequence.html).)

I had a tremendous amount of fun while working in F#, but a few things kept nagging at me.

## What the...

Right off the bat, I missed Haskell's equivalent of type classes, which surprised me. In OCaml, [functors](https://realworldocaml.org/v1/en/html/functors.html) and modules are [roughly equivalent](http://conway.rutgers.edu/~ccshan/wiki/blog/posts/Translations/) to type classes, modulo loss of some brevity. In F#, the only alternative seems to be [a combination of object-oriented interfaces and dictionary passing](https://web.archive.org/web/20081017141728/http://blog.matthewdoig.com/?p=112), which seems unpalatable to me -- especially since this solution does not preserve type safety.

To be fair, there is indeed limited support for generic arithmetic (for example, via [static constraints](http://msdn.microsoft.com/en-us/library/dd233203.aspx)). Nonetheless, I found it awkward to deal with. It must also be admitted that OCaml is no better in this regard (c.f., the famous `+.` floating point operator).

I also found myself annotating more than I thought I would have to. Perhaps this is due to the slightly unusual finger tree type structure, but it did feel like [type inference](http://lorgonblog.wordpress.com/2009/10/25/overview-of-type-inference-in-f/) was [not as strong](http://stackoverflow.com/questions/3162387/why-is-fs-type-inference-so-fickle) as it could have been.

Coming from Haskell, I also hit the dreaded "[value restriction](http://en.wikipedia.org/wiki/Value_restriction)." Because values are prohibited from being generic, I found myself unable to eta-reduce to point-free functions. (You can certainly add monomorphic type annotations, but that rather defeats the purpose.)

## Damn You, Haskell

While frustrating, the issues above are understandable because F# is constrained by the CLR (no type erasure), its ML heritage, and OO paradigms. I did not see any crippling defects in the language itself. So I do not begrudge F# these flaws.

Really, I would not have noticed most of these limitations even a few years ago. Up until now, I had not realized how pervasive and thorough Haskell was in terms of re-writing my programming language perspectives.

Leaving pernicious Haskell influences aside, F# is really a fine language in its own right.

## The Delights of the Garden

I have covered my major annoyances, so it is only fair to talk about these features I was thrilled to find:

- [Operator overloading](http://en.wikibooks.org/wiki/F_Sharp_Programming/Operator_Overloading). Yes, operator overloading can be abused. But it is so, so convenient. I missed this in OCaml.
- [Units of measure](http://msdn.microsoft.com/en-us/library/dd233243.aspx). Aw, yes. I would love to see more of this in other languages.
- [Active patterns](http://fsharpforfunandprofit.com/posts/convenience-active-patterns/). Haskell has the flexible [ViewPatterns](https://ghc.haskell.org/trac/ghc/wiki/ViewPatterns) extension, but for some reason, I found active patterns in F# easier to use.
- [Query expressions](http://msdn.microsoft.com/en-us/library/hh225374.aspx). LINQ in F#. Enough said.

I did not have enough time (there is never enough time, alas) to plumb deeper depths. I would have liked to explore F#'s inter-operability with other CLR languages, for example.

All that being said, my exploratory research was conclusive in at least one regard: I will be promoting and using F# for work (one of the few advantages of [leading a startup](http://www.openhorizonlabs.com/)!)

There is no doubt in my mind that F# is ready for prime time.

## References

During my journey through F#, I was guided by a [few hundred StackOverflow posts](http://stackoverflow.com/questions/tagged/f%23) and a couple of books.

[Expert F# Programming](http://www.apress.com/9781430246503) is a passable reference book, but it did not do much for me beyond elucidating some design decisions. But then again I am probably not in its target demographic. I can see, however, how it may be useful for newcomers to the ML world. The second book I consulted was [F# Deep Dives](http://www.manning.com/petricek2/), and though this book is still in preview mode, I can recommend it whole-heartedly: one of the few books about F# that focuses on practical, real-world usage.
