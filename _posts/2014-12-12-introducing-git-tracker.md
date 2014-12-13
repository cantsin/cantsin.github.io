---
layout: post
title: Introducing git-tracker
comments: true
date: 2014-12-12
---

<blockquote>
<p style="margin: 0px;">the self isn’t a historical fiction or a cultural construct</p>
<p style="margin: 0px;">or a linguistic hallucination;</p>
<p style="margin: 0px;">the self is a creature</p>
<p style="margin: 0px;">and it lives in a burrow</p>
<p style="margin: 0px;">under the hillside of history</p>
<p style="margin: 0px;">&nbsp;</p>
<p style="margin: 0px;"><a href="http://www.poetryfoundation.org/bio/tony-hoagland">Tony Hoagland</a>, "Still Life"</p>
</blockquote>

## And The World Needs This Because...

I have long struggled with keeping and tracking personal data metrics, despite (and perhaps because of) the glut of hardware and software metrics products. It seems like obtaining meaningful statistics about one's overall activities should be easier. For some reason, it is not.

Git is a natural candidate for promoting metrics tracking, since it is so prevalent in the programming world. Furthermore, all of my writing is under git control, including my journals and to-do lists.

Currently, I track my git usage using [git_stats](https://github.com/tomgi/git_stats), and of course there is the all-pervasive and public GitHub heatmap (available on an user's "[view profile](https://github.com/cantsin)" page). But these tools are of limited utility.  `git_stats` has a whole lot of [irrelevant statistics](http://tomgi.github.io/git_stats/examples/devise_invitable/files/by_extension.html), and not all of my projects are on Github.

<!--more-->

## A Three-Pronged Attack

I enjoy reading articles about the [quantified self](http://quantifiedself.com/) and it seems like most people end up implementing their own tools and workflow to accommodate their [personal quirks](http://quantifiedself.com/2014/12/ian-billett-tracking-time-life/) and [idiosyncratic practices](http://quantifiedself.com/2014/11/bryan-ausinheiler-diet-digestion/). Clearly, I am no different in that regard, since I am designing my own data metric tools.

`git-tracker` is the first step in my data gathering efforts. I realized recently that my efforts were a bit too ad-hoc to allow for consistent and regular data collection. So I took a step back and defined three broad categories I wanted to capture: projects, health, and communication. All of them have quite different collection needs.

Projects, fortunately, is by far the easiest category to tackle. As I have alluded to above, everything is in git. Tracking health metrics would involve a collection of online services and personal notes (such as records of rock-climbing attempts). Tracking communication habits necessitates the use of passive monitoring technology such as the stealth [SelfSpy](https://github.com/gurgeh/selfspy).

## Oh, The World I Dream Of

In an ideal world, my statistics would be hooked up as raw data to play around in [IPython Notebooks](http://ipython.org/notebook.html) (shades of Mathematica and Matlab). [Pandas](http://pandas.pydata.org/) is simply awesome, although I am itching to try out the [IJulia](https://github.com/JuliaLang/IJulia.jl) kernel. In any case, it should be easy to create graphs of all kinds and to share them (to a limited extent).

And of course, in this Utopia, all of my data should be easily accessible and under my total control, with permission controls and locks, should my [health insurance want this information] (http://gearpatrol.com/2014/09/19/caution-in-the-age-of-the-quantified-self/). God forbid I need multiple logins to multiple services using [OAuth1](http://oauth.withings.com/api) and [OAuth2](https://jawbone.com/up/developer) to retrieve [scattered](https://developer.nike.com/documentation/api-docs/activity-services/gps-data.html) [data components](https://wiki.fitbit.com/display/API/API-Get-Glucose). Assuming, of course, that the data is even [available](http://www.dcrainmaker.com/2014/03/garmin-vivofit-review.html).

## Reality Is A Harsh Taskmistress

The basic idea of `git-tracker` is to track progress and projects based on 'activity' (and not some [misleading metric](http://stackoverflow.com/questions/3769716/how-bad-is-sloc-source-lines-of-code-as-a-metric) such as lines of code or commits). For my personal projects, 'activity' once per day is sufficient -- as a friend often says, "If we do not take a step every day, the journey can become effectively infinite." For my writing endeavors, measuring lines is indeed a valuable metric. For work-related projects, it is more interesting to see how productive and effective I am in a given language and domain.

While I could have displayed my data using any number of graphical plots, I chose only the two I thought were most useful: [Heat Maps](http://en.wikipedia.org/wiki/Heat_map) and [Tree Maps](http://en.wikipedia.org/wiki/Treemapping). Heat maps are best suited for tracking patterned usage and tree maps are useful for visually partitioning hierarchical data.

Add a lightweight tag system to the mix, and you have [git-tracker](https://github.com/cantsin/git-tracker). It is still a work in progress as of this writing.