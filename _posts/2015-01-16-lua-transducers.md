---
layout: post
title: Lua Transducers
date: 2015-01-16
---

> All God does is watch us and kill us when we get boring. We must never, ever be boring.

> Chuck Palahniuk

Transducers are one of the cooler bits in [Clojure](http://clojure.org/)-land. If you are new to transducers, don't worry: with a bit of experimentation, they become straightforward and easy to understand.

Recently, I [implemented transducers](https://github.com/cantsin/lua-transducers) in [Lua](http://www.lua.org/), partly because I was curious as to how the underlying implementation works, and partly because I was wondering how they would work with Lua's iterators (which are really just [closure factories](http://www.lua.org/pil/7.2.html)).

<!--more-->

## What Are Transducers, Again?

[The official description of transducers](http://clojure.org/transducers) is unfortunately a bit abstruse:

> Transducers are composable algorithmic transformations. They are independent from the context of their input and output sources and specify only the essence of the transformation in terms of an individual element. Because transducers are decoupled from input or output sources, they can be used in many different processes - collections, streams, channels, observables, etc. Transducers compose directly, without awareness of input or creation of intermediate aggregates.

While certainly correct, this description does not tell us much.

Transducers are premised on the notion of a reducing function. A reducing function is a function which accepts an element and a previous reduction, and returns a new reduction. Basically, it is the function you would pass to a `reduce` or `fold` call. The type of a reducing function would be `(r -> a -> r)`.

In the following Lua code,

    reduce(operator.add, 0, {1,2,3,4})

This particular `reduce` call returns `10` as the result. `0` is the 'seed' given to the reducing function, `operator.add`.

Transducers are a function that takes a reducing function and returns another. The type of a transducer would be, loosely, `(r -> a -> r) -> (r -> a -> r)`.

## One More Thing...

Recall that `reduce` is fundamental in that it can be used to implement [`map`](http://blog.lerner.co.il/implementing-filter-reduce-ruby-python/) and [`filter`](http://blog.lerner.co.il/implementing-filter-reduce-ruby-python/). So reducers are indeed fundamental in the sense that they are basic building blocks for transforming input streams.

In Clojure, there has been a steady attempt to disentangle the source of data and the operations that might apply to it, first with [reducers](http://clojure.com/blog/2012/05/15/anatomy-of-reducer.html) and now transducers. Today, in Clojure 1.6 and beyond, most sequence functions have an arity that produces a transducer. For example, `(remove odd?)` returns a transducer that removes all odd integers.

## Okay, So Why All The Fuss?

Well, personally, I think all the fuss about transducers is overdone. But there *are* a few neat things about them. First, transducers can be composed using regular function composition. Second, transducers are decoupled from sequences (as the official description says). These two properties mean that it is easy to create an arbitrary chain of transducers that will iterate over the sequence (be it a list, observable, or what-have-you) exactly once.

In other words, you can do the equivalent of a few dozen `map` and `filter` calls, and optionally `reduce` it all without iterating over the sequence repeatedly. (Of course, if the sequence is eventually reduced to a single value, there's not much more to be done for subsequent transducers.)

Given the transducers `remove`, `map`, and `take`, the following Lua transducer

    compose(remove(odd), map(plus1), take(5))

operates on any given stream, element by element. For each element: if it is odd, it is discarded; otherwise `1` is added (thereby making the number odd again); if the transducer now has five (formerly even) elements, the processing stops.

A few things to note. Composition of transducers is applied left-to-right, meaning that the `odd` transducer comes first. Additionally, a transducer such as `take` breaks out of the iteration early, meaning that this transducer would stop immediately after the fifth even number is processed. Again, these transducers do not deal with sequences directly. They operate only on the level of a reducer, which takes in one element and the previous reduction at a time.

This behavior is neat, particularly if you have to deal with a lot of sequence processing.

## Formalize It For Me, Baby

Well, OK. Transducers are essentially [Kleisli compositions in the List monad](http://stackoverflow.com/questions/26653829/how-is-a-transducer-different-from-a-partially-applied-function). Transducer composition is also equivalent to monad-arrow composition.

This [blog post](http://conscientiousprogrammer.com/blog/2014/08/07/understanding-cloure-transducers-through-types/) helps clarify a lot of the types around transducers, and gives a more formal type (`(r -> a -> r) -> (r -> a -> r)` is not quite correct -- you need rank-2 types).

## Back to Lua

My implementation parallels that of [transducers-js](https://github.com/cognitect-labs/transducers-js) (though I do not focus on high-performance). In addition, I implemented only a few transducers, these that I thought were most useful.

In particular, a reducer (in the Lua code, 'transformer') protocol requires three functions: `init`, `step`, and `complete`.

`init` is called by the `transduce` function (and then only for the first reducer), `step` is a standard reduction function, and `complete` is defined for these reducers that want to produce a final value.

Recall, once again, that transducers take in a reducer and return a reducer. For the vast majority of transducers, `init` and `complete` are delegated to the input reducer. So implementing a transducer basically boils down to implementing the `step` function that it will return (as a reducer).

I follow the [Clojure specification](http://clojure.github.io/clojure/branch-master/clojure.core-api.html#clojure.core/reduced) for early termination of `reduce`.

An example to round everything off:

    local transducer = f.compose(t.drop(1), t.take(2), t.drop(1))
    local result = t.transduce(transducer, tr.append, {}, {1,2,3,4})
    -- { 3 }

I think [the Lua transducer code](https://github.com/cantsin/lua-transducers) is short and straightforward. Implementing transducers was a fun exercise and helped me to understand them on a deeper level.
