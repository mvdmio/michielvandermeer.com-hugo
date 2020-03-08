+++
title = "Bite Sized Refactoring"
date = 2019-10-27
feature_image = "/images/blog/dawn-desktop-background-dusk-36717.jpg"
author = "Michiel van der Meer"
tags = ["Software"]
+++

Sometimes, when I'm refactoring, I end up with a PR that has way too many changes. It starts small, often just a single method I'd like to change. But that method is called in another class that has other things I'd like to change as well. Before you know it, the changes are cascading through the code base and the changeset starts to bloat.

When my colleagues see a PR with such a changeset, they understandably get a bit upset; and they should!

In this article I'd like to explore what you should do when refactoring, and what you should do when someone like me hands you a big PR with lots of changes. Let's start with that last one.

## What to do when you receive a big refactoring PR
Reject it!

Seriously. Reject that PR. It should not be merged and it should not waste your time on a review.

The problem with large changesets is that they have unforeseen side effects. Even if you know the codebase inside and out it's almost guaranteed that you're going to miss something. That something will then become a bug. That bug will become a problem; often sooner rather than later. As soon as it becomes a problem, it becomes more work; work that was not planned and would not have been necessary if you would just have rejected the PR.

Every change is a potential bug that will cascade through the project and eat up all the time you had to work on the feature. Before you know it, the sprint is over and your feature isn't done.

Now, rejecting large PRs will upset the person who worked on that PR for a week. That's OK. Of course it's not fun when your work gets deleted. But it's even less fun when your work holds up everyone on the project because it created a bug. On the flip-side, having your work deleted is a good way to learn to keep your changesets small.

## What to do to get your PR accepted
Now that you know that your PR will get rejected if you make too many changes, let's focus on what to do to get your refactoring actually accepted.

### 1. Small change sets
The first thing to do is make your change sets small. I mean one-file small, or as close to it as possible.

According to [Martin Fowler](https://martinfowler.com/), _Refactoring is a disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior_ [[1]](https://refactoring.com/).

If you follow this definition very strictly, then you should have an easy time changing only a single file. Only changes to the public members of a class would actually force you to change multiple files.

Unfortunately that doesn't help us much. Often changes to the public members of a class are needed to clean up the code base, so I often follow Fowlers definition a bit more loosely. I see the internal structure on the level of my application, not on the level of each individual class.

In any case, if you're making changes to the public members of any class, follow rule two:

### 2. Only make a single API change at a time
The public members of a class can be called its API. Don't confuse this with the application API that exposes endpoints for other programs or clients to consume.

I would advise you to only change a single class API per PR. This will limit the file changes to a handful of files. All these changes will have the same reason: the same single API change. This will make it much easier to understand the implications of the change in each part.

### 3. Increase the frequency of the small change sets
Follow these two rules and you'll make much more focussed improvements to your code base. All that remains is to do these changes a bit more frequently so that the code base keeps improving over time.

You'll see that small PRs will cause less bugs, improve the quality of the code and make the life of the code reviewer(s) much easier.