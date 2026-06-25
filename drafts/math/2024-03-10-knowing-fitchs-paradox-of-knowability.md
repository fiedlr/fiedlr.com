---
title: Knowing Fitch's Paradox of Knowability
author: Adam Fiedler
teaser: "The other day, I was reading the amusing little book What We Cannot Know by du Sautoy (I highly recommend!).
It mentions a beautiful idea called Fitch's Paradox of Knowability, that is originally attributed to Fitch but supposedly originated in Alonzo Church's mind.
In this post, I would love to share my thoughts.
"
tags: logic, paradox, knowing
---

There's lots of talk about learning in the context of neural networks.
However, it is beautifully simple to model "learning" in modal logic.
Once we do model it this way, it gives us a curious paradox about knowability.

# Epistemic Modal Logic
We can use the so-called epistemic modal logic, whose syntax is as follows:
`phi ::= p in Prop | p /\ q | not phi | K phi | L phi`
where `p` are propositional variables and `L` (possibly) and `K` (known) are modal operators.
`LK phi` should therefore mean that `phi` as a statement is possibly known,
i.e., knowable.

Modal logics are usually interpreted using Kripke semantics, where a model is
a simple digraph composed of nodes as our states (also called possible worlds) and modal
operators are simply transitions, a means, to traverse between the nodes (states).
A "frame" is a model that also assigns to each state true propositions,
these are usually denoted `p`, `q`, `r`, and so on.
`K p` would mean in Kripke semantics that such a state is *reachable* through
a `K`-edge where `p` is true.
Reachable from where? Kripke semantics is a bit more nuanced, but
this is just an intuition and more details are not needed for this article.

For simplicity, we can say that a statement in modal logic is true if and only if
it is true in all the models (and thus, i.e., in all the frames).
Obviously you want to model only such statements (meaning have such statements
true) that make sense in some regard to epistemics.
Can I say `LLLLLKp`?
This is where axioms come in and they say what kind of models we're considering.
In some sense, they are predetermining which statements using the above syntax
make sense at all.

# Example of An Unknown Truth

So is there a true and unknowable truth if we look at it in epistemic modal logic?
Here is the version I am borrowing from du Sautoy (I hope it's ok!).
Let's say you're looking for your socks, and you're wondering whether they are in your bedroom.
If we are okay with the axiom of the excluded middle (LEM), there are two choices:

1. Socks are in my bedroom.
OR
2. Socks are not in my bedroom.

Now, we know that 1. or 2. must be true (by the axiom of the excluded middle).
Let us assume that the propositional variable `p` represents the true statement
of these two.

Here comes the puzzling part.
Consider the statement:
> `p` /\ not K p
> `p` is true and `p` is unknown. (*)

Remarkably, this statement labeled as (*) is *itself* is indeed true, and indeed unknowable:

> not L K(`p` /\ not K p)

Why?!
It seems to be a circular argument, doesn't it?
Also, we know that `p` is either 1. or 2.!

It is not circular, in fact, it is perfectly provable in modal logic with basic axioms.
However, I'd like to try explaining this intuitively why that is the case.

Let's first show why (*) is true.
This statement is true because we do not know what `p` is, but we know represents the correct choice of 1. or 2.
This is easy.
Why is (*) unknowable though?

Note that we can find out what `p` is, simply look for your socks in your bedroom.
The issue is different: we cannot know what (*) itself is.
Let's try to prove me wrong, we can simply try all the cases, right?
Let's say `p` points to 1.

> "Socks are in my bedroom" /\ not K ("Socks are in my bedroom").
> "Socks are in my bedroom" is true and unknown.

But this is false, because `Socks are in my bedroom` is known (we assume
`K p`)!

You probably see the rest.
Let's say `p` points to 2, then we get
> "Socks are not in my bedroom" is true and unknown.

But then this is false, because again, everything is known.

By proof of negation, we must conclude that (*) is unknowable.

# Where is the paradox?

Now we know that there indeed is a sentence that is an unknown truth.
Why is it a paradox?
It is a paradox because (*) is true but unknowable, and it is curious what this means.

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
