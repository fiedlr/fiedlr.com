---
title: Knowing Fitch's Paradox of Knowability
author: Adam Fiedler
teaser: "The other day, I was reading the amusing little book What We Cannot Know by du Sautoy (I highly recommend!).
It mentions a beautiful idea called Fitch's Paradox of Knowability, that is originally attributed to Fitch but supposedly originated in Alonzo Church's mind.
In this post, I would love to share my thoughts.
"
tags: logic, paradox, knowing
---

It is beautifully simple to model "learning" in modal logic.

# Example of An Unknown Truth

So is there a true and unknowable truth?
Here is the version I am borrowing from du Sautoy (I hope it's ok!).
Let's say you're looking for your socks, and you're wondering whether they are in your bedroom.
If we are okay with the axiom of the excluded middle, there are two choices:

1. Socks are in my bedroom.
2. Socks are not in my bedroom.

Now, we know that 1. or 2. must be true (by the axiom of the excluded middle).
Let us assume that `p` points to the true statement

Here comes the puzzling part.
Consider the statement:
> `p` is true and unknown. (*)

Remarkably, this statement *itself* is indeed true, and indeed unknowable.
Why?!
It seems to be a circular argument, doesn't it?
Also, we know that `p` is either 1. or 2.!

It is not, in fact, it is perfectly provable in modal logic with basic axioms.
However, I'd like to try explaining this intuitively why that is the case.

Let's first show why this statement is true.
This statement is true because we do not know what `p` is, but we know it points to the correct choice of 1. or 2.
This is easy.
Why is (*) unknowable though?

Note that we can find out what `p` is, simply look for your socks in your bedroom.
The issue is different: we cannot know what (*) is.
Let's try to prove me wrong.
Let's say `p` points to 1.

> "Socks are in my bedroom" is true and unknowable.

But this is false, because `Socks are in my bedroom` is known!

You probably see the rest.
Let's say `p` points to 2, then we get
> "Socks are not in my bedroom" is true and unknowable.

But then this is false, because everything is known.
By proof of negation, we must conclude that (*) is unknown.

# Where is the paradox?

Now we know that there indeed is a sentence that is an unknown truth.

# Appendix

How can we prove (*) is unknowable in modal logic?

`(p /\ not K p) /\ not K(p /\ not Kp)`

`p -> K p`

`Kp -> KKp`

`p -> K p`
`not K (not (p -> K p))
`not K (p /\ not K p)`

We just showed that
`K (p /\ not K p)` and `not K (p /\ not K p)`, which is `bot`.
Proof of negation yields `not K (p /\ not K p)`, i.e., (*) is unknown.
