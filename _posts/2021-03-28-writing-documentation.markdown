---
layout: post
title:  "Writing Documentation"
date:   2021-03-27 13:50:00 +0200
categories:
---

Writing documentation is the kryptonite for software engineers. It's this thing we have to do after we finish all the interesting work and since we did all the interesting work we know everything about it so why do we need to document it? This idea it's definitely exaggerated but I did have a version of these feelings in my first years as a software engineer. And this is ironic because during that time the top learning place for me was actually documentation (I remember always having a tab open with the Django documentation site). There was difference though - it was __good written documentation__ that was helping me while I was writing and dreading the bad kind.

Later in my career I had the chance to take on a project of documenting a large codebase (300K lines of code, 150 services) from the position of the person who knows the most about it as I've been part of the team for 5 years and the feedback I got on the documentation was very positive. The principles that helped me were strangely close to the way a good software product is built. Here are some of them.

## Customer Research

You have to know your customers! Is your documentation for other developers? If yes, is it for new joiners? Is it for senior members of the team? Do product people read this documentation?

All these questions are valid ones and if you ask people from each category they will definitely say they need some documentation and things can go out of control. As with real customers it's better to observe their behavior. Good places to observe your customers are:

* your company chat - a lot of noise in there but there should channels dedicated for questions
* team stand ups - probably the easiest and most valuable since people talk about their blockers
* planning sessions - there will be higher estimates when unknowns are involved
* all software engineers - if documentation is missing people are the source of information, make a pact with all the people in your team to take notes on questions they get asked an group them in user categories

## Putting Customer Research Together

In my case research showed that people usually look to put ideas in context and information about processes we collectively put together but never documented and audience was mostly software developers. The categories I stared with were:


### Team Principles

Each team has to have some principles. This section outlined ours and gave the context around them. For example, we were in the middle of migrating to Go from Python and one of our principles was `Any new service has to be written in Go`. Principles in general help to solve debates on tech solutions. Whenever you have two solutions they will give you a framework to evaluate them. I guess this is a topic for another blog post.

### Technical Overview

This section gives a birds high view of how the project is implemented. This is a good place to state any frameworks you're using, communication protocols, database technologies etc. Don't get into too much depth about the technologies, you can link to their official documentation page so people can go read about them.

This part may include **system diagrams**. We'll discuss about how to manage these below.

### General practices

Here is an overview about how the team works. How we do planning, how we run the daily standup, TDD, BDD and any other things people need to know about working with the team. You can think about this as an extended contributing guide.

### How to guides

Documentation is this section will be the response of "How do I do X?" where X can be pretty much anything. We added documentation for running database migrations, managing testing accounts, running a CI job etc.

This section will get the most changes in your project's lifetime.

### On-call Runbooks

If you are on-call you don't want to lose time to go through all steps of a how to guide. You probably already know most of the things since you are expected to wake up during the night and solve problems. THe runbooks are here to help you with ready to run commands without a lot of context around them.

## Organizing documentation

Think about a well designed product, your Netflix or Google or Amazon. Everything you need seems to be one click away, you never have to figure out how to start a new show or find the shopping cart. It is all about user experience and it's the same with documentation. You don't want to have to remember were documentation for running migrations is. Is it in the database folder? Is it Confluence? Is it in Github or Google docs? Anything that you write will be of no use if it can't be found. For this as well, there are a couple solutions

### Any document must be accessible from the documentation index page

The first idea here is having an index page. This serves as a starting point for anyone who has a question. It doesn't mean we need a huge index file, the access can be indirect but you have to be able to get to the document starting from the index page. If you don't link your documentation it will be like dark web.

### Bring documentation to your users

It's nice when Netflix knows what you want to watch. It probably involves some complicated algorithm and tons of data so it's not worth implementing it for a dcoumentation site. But we do know when we need to know something, we can give our users a better experience if we explore this knowledge:

* documentation for the lifetime of a pull request should be there when you open the pull request (Github templates help with this)
* documentation for on-call alerts should be there when you get paged (you can link it in alerts)
* coding related decisions must be documented with the code not in a different file

I'm sure you can find a lot more examples for your team. You will see that it saves a lot of time getting everything when you need it.

### Documentation has to be searchable

Is great that people can access documentation from the index page but what if there is an easier way? Usually, when you don't know something you search for it on the web. This is true for documentation as well and an important principle here is **keep your documentation in one place**. You don't want to spread your docs on 3 platforms because you will never be able to search it in one go even if it's accessible from one index page.

As per the previous section, some documentation is useful to be in the code and most of the questions start from people reading the code and looking for more information. I would extend the principle above to **keep your documentation and code in one place**. This way, if you search for something code related you will find both code and documentation references.

My project was in a monorepo so it wa very easy to implement the principle above, we just had a `docs` folder for individual files and used the root `Readme.md` as index. This works in a multi repo as well if you have a `documentation` repository. People will search for code references across the whole Github organization anyway so documentation results will be surfaced.

## Prepare for change

As any good product, your documentation will evolve over time. You need to be prepared to keep documentation up to date with as low maintenance effort as possible.

### System Diagrams

Every time I worked on a diagram it was outdated by the time I finished. There are a lot of people working on a system and it will change faster than any visual representation. Unless you automate generating the visual representation. If you are using Kubernetes you probably already have a CNI that shows a live diagram of how your system components communicate with each other. This probbly does not work in a pub-sub architecture but it can't be solved with proper monitoring. If you log in your monitoring system the OUTs and INs in your services it's pretty easy to generate a diagram using the system's API and [plantuml](https://plantuml.com/) or a nice javascript library for generating graphs.

### Code Documentation

Code changes most often and we almost always forget to update documentation in some md file. If there are code particularities they should be documented near the actual code instead of a file somewhere in the documentation folder.
Even better, **try to document it in a test**. Tests are the best way of documentation behaviors and corner cases, if the behavior changes we know we have to update our documentation because it fails.

### Update processes

If documentation was not a priority for a while people will not be used to think about maintaining and improving it. You should update your planning guidelines to include maintaining documentation for each project.

### Feedback Loop

Have a way to get feedback from your peers on the documentation. The easiest way is to include it in the Developer Experience poll if you have one, or start one in case you don't.

## Socialize it

As with any product you need to sell it. Share it on your company chat, try to respond questions with link to documentations, talk with the other developers to do the same. The more people you get on board, the more value it brings.
