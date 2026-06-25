---
title: The Era of Specification-Driven Development
author: Adam Fiedler
teaser: "People tend to say that AI is bringing programming to a higher layer
of abstraction: the human language. However, there's a big elephant in the room.
Any human language is vague. I argue here that the next layer of abstraction
might as well be formal specifications grounded in logic.
We can build apps around specifications and let agents generate code that satisfy
our specifications.
Our specifications also determine what kinds of decisions about code we delegate
to the LLMs.
This is why specification-driven development is more relevant now than ever.
"
tags: ai, logic, verification, testing, fuzzing, specifications
---

Everybody who studied mathematics or computer science in a bit more detail
should realize that human language suffers from vagueness and ambuiguity.
Not only AIs tend to hallucinate, we ourselves tend to phrase things imprecisely.
Consider the following prompt:

```markdown
Make an app that plays Moonlight Sonata two times.
```

Let's say the AI is smart enough to ask us what kind of app, on what platform, etc.
The LLM goes ahead and creates the app for us, but the app plays the song three times.
Surely the AI must have hallucinated?
The answer is that the app is perfectly fine because our request is met: the app plays Moonlight Sonata (at least) two times.
A person has to have formal training in order to understand that an LLM can decide on its own how to interpret such a sentence.
If we don't understand this distinction in language precision, we cannot possibly know how to delegate mission-critical apps to AI agents.
There are two points I will be trying to make:

1) The human language *alone* cannot serve as *the basis* for app building because it lacks precision.
2) Our understanding cannot be replaced by an LLM. We should be aware of what decisions we are delegating and I'll be sharing my thoughts on how.

As a note, I'll be saying the word "app building" to mean any sort of activity that produces a piece of software.

# The Problem

We cannot resolve this matter with adding more and more "rules" or "skills".
Think of it like this: an English sentence limits the number of possibilities for a generated code, but even if the AI does not hallucinate on its own,
the number of possibilities is simply always too big.
And the most important thing:

> By putting English sentences in a context, you do not necessarily make the space smaller!

Consider the following prompt.

```markdown
- Make an app that plays Moonlight Sonata two times.
- The app should not play Moonlight Sonata three times.
```

The LLM goes ahead and creates such an app, but the app plays three times again.
Can you see why?

It's even worse.
More rules can under some contexts lead to a bigger space of possibilities.

```markdown
- Make an app that plays Moonlight Sonata exactly two times.
- The app should allow some users to play Moonlight Sonata three times.
```

If it's not clear how this prompt can make the situation worse, let me know in the comments.

Again, we need to have formal training in logic to understand this.
Again and again, AI cannot replace our understanding.
If you leave everything to its whims, you are not really building your app but just playing a slot machine.
It also doesn't matter how many LLM judges we have because thay also make decisions on their own.
How do we get around this?

> Our LLM agents will inevitably make decisions for us.
> This is fine for some decisions, but not for all of them.
> Our task is to *think ahead* what decisions we leave up to the LLM.
> We can do this by *determing the properties* we expect and specifying them in a formal way.

We should think ahead of time what properties should definitely hold and enforce them by specifying them in a precise way (ideally not in a human language).
This way we know what decisions we are delegating and what properties to check for in our app before we start building.
And this is nothing else than the good old *specification-driven development*.

# The Specification-driven Workflow

We specify properties first, then we write code and/or let the agents generate code.
We specify properties first especially because we want to use AIs to produce code for us.
This is why specification-driven development is more relevant now than ever.
In an ideal world, we then *verify* these properties using a verifier.
Verifiers are special programs that can take a property in some formal language as input and *guarantee* that this
property holds for a given program.
As the LLMs cannot replace our own understanding, they cannot write the specifications for us.
We cannot prompt our way out of this.
However, you do not need to be trained in logic to start.

We make a full circle and go back to the thing we all find annoying: testing.
Tests are the only way to keep anyone grounded in what an app is actually doing.
They are not a replacement for verification (e.g., see my [article on this](https://adamfiedler.com/verification/2022-11-02-warning-code-can-be-explosive)) but
they are essential especially in this day and age.
The workflow I'm suggesting is built on top of test-driven development (TDD) as follows:

1. We ourselves have to give the specifications for the code at a proper level of abstraction.
2. For these specifications, we should write the skeleton of the most crucial tests ourselves (it can totally be assisted by an LLM, but not vibe-coded).
3. We write the code that satisfies the specifications in 1) and the skeleton tests in 2), and/or let agents generate some parts of it.
4. We transform the test skeletons to real tests.
5. We cover more test cases using *fuzzers*. Fuzzers are much more effective in covering a huge area of choices than letting AI generate test cases for us.
6. Only after we ran out of options with fuzzers, we can vibe-code generate numerous additional test cases using LLMs.
7. We iterate code modifications until all the tests pass.
8. We should continually run and maintain our test suite to make sure that properties given by our specifications hold.
9. We formalize the specifications once the main components of our code are fixed.
10. We should continually verify the crucial components of our implemented app using verifiers, or get *a person* who can do it for us.

Test skeletons might be tricky to come up with before you see the code, but that is the point.
They force you to think about the problem ahead of time.
One can get enough experience to choose the right level of abstraction for the specifications
that you write before any code is programmed and/or generated.
I might be dealing with this in some other article.

However, keep in mind that specification-driven development doesn't necessarily require TDD.
The essential part here is to come up with specifications first, think of the properties first.
You can choose to what extent and how you formalize these specifications ahead of time.

# The Take-aways

To sum up, these are the main points I have been making here.

- Human language alone is too imprecise to serve as a basis for app-building.
- We have to think ahead of time about the properties and specify them *formally* as specifications.
We cannot do this post-hoc if we want LLMs to generate most of the code.
- By giving our specifications, we essentially design and determine the main properties we expect from our app.
If we let AI do it for us, we essentially say we do not bother making decisions anymore.
- By giving our specifications, we also determine what sort of *decisions* we delegate to the LLMs.
- The specifications can contain "bugs" if they imply unintended consequences, and this is why formal training is still necessary. We can still be in a better place by thinking about tests thoroughly. If we do not have the experience with verification, we should turn to someone who can for the critical parts.
- We should start building an app around tests. To let an AI generate an app and produce *all* the tests for it is like playing a slot machine.

If you are interested more in this approach for your company, I'd love to hear your thoughts.
Let's connect on LinkedIn, comment there, or feel free to write me an e-mail.
