---
title: Machine Searching Machine
author: Harsha Vardhan
date: 2018-05-02T06:56:15+00:00
draft: false
slug: machine-searching-machine
categories:
  - technology
  - ai
tags:
  - alterego
  - app ideas
  - apps
  - google assistant
---

*Editor's note (2026): Re-reading this in the age of LLM-powered agents, 
RAG, and function-calling — this 2018 idea of "machine searches machine" 
based on translated intent and capability matching is essentially describing 
what agentic AI systems do today. Wild to see this from 8 years out.*

---

[This question][1] was originally posted on Quora. I had posted an answer 
there and then thought of making it a part of my blog as well.

## What apps do you wish someone would make for you?

While framing the answer I felt this had the potential for a great design 
discussion — it was opening gates to many ideas with great flow charts. In 
order to not let it explode, I tried to keep my answer brief. If anyone is 
interested, I am all sport for a discussion further.

Seriously, with so many apps in the market, it has become an Amazon-like 
jungle with many trees and fruits — where we know (or at least have a hunch) 
the fruit exists, but the challenge is how to find the one you are looking 
for. The fruit is something you can hypothesize, and most probably it would 
already exist quite close to your imagination. But how do I reach it? Suppose 
I found a fruit which appears like the one I was thinking of — I don't know 
it for sure unless I taste it, and worse, when I taste it I realize that's 
not what I wanted. Should I re-imagine a different fruit or try a different 
similar-looking one? Thinking about apps suddenly appears pretty complex.

## Breaking into sub-problems

The way I would further break the problem into sub-problems:

1. When would I know I might need an app? How would I know what I am thinking 
   can be helped by an app?
2. If I am sure of what I am thinking, how would I create a proper search 
   string to find it?
3. How would I be sure that the search string I have created is exactly how 
   the app publisher would have tagged it to be searched?
4. When I am given 1000+ choices, how would I find the right one without 
   trying them one by one?
5. Because I don't know which apps exist, I might not even know there is an 
   app for the problem I am thinking about — and so I might never search for 
   it, and just live with whatever recommendations come my way.

## One potential solution to address the above

I guess we should use something like **[AlterEgo][2]** — a device in 
evolution, which is growing the capability of reading our thoughts.

{{< youtube RuUSc53Xpeg >}}<br>

Now modify it a bit for our use case. Let's feed this thought to an AI 
system which breaks the need into "app capabilities" I am looking for, and 
makes the search for me. This search will be more like "machine searching 
machine," and I hope for better chances of mutual understanding here 😉. 
Sounds crazy, but if you try to design it, it would make sense. Now the 
question is — search where? We have all systems designed to be searched by 
humans. Great, let's make that too.

**A Google-like search for machines:** while publishing an app, it would be 
tested by AI bots and their capabilities would be fed to a database before 
being uploaded to any app store. There would be a many-to-many relationship 
between apps and their capabilities — the database captures the mapping of 
capability to corresponding apps.

There you go:

<div style="background-color: #f0f4f8; border-left: 4px solid #4a90d9; padding: 16px; border-radius: 4px; margin: 20px 0;">
You think something <br>
---> <b>AlterEgo</b>-like device reads it and feeds it to a 
machine learning engine <br> 
---> This engine translates what you need into 
capabilities <br>
---> A Google-search-alike for machines returns the app(s) with the highest 
capability match score.
</div>

I guess this is what I would want as an app to do for me — my search app. I 
am not sure if this is the future of [Google Assistant][3].

-Cheers,
Harsha Vardhan

[1]: https://www.quora.com/What-apps-do-you-wish-someone-would-make-for-you
[2]: https://www.youtube.com/watch?v=RuUSc53Xpeg
[3]: http://assistant.google.co.in/