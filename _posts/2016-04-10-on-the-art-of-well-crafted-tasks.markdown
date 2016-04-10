---
layout: post
title:  "On The Art of Well Crafted Tasks"
date: 2016-04-10 21:55:00+10
cover: "office_stuff_tim_gouw.jpg"
cover_artist: Tim Gouw
cover_link: https://unsplash.com/photos/KigTvXqetXA
tags:
---

It's now common practice in software development circles to use issue tracking software to keep track of work being done. There are some full featured offerings available, such as Jira and Asana, as well as more humble tools available such as Trello, or GitHub Issues. However, something that perhaps isn't pointed out often enough is that there's a bit of an art to writing a good task.

{% include captioned_gfycat_image.html gfycat="HappyAbleBobwhite" caption="'Bulk Load', 'Rules Based Filtering' and 'Ingestion Telemetry' sound more like search terms than actionable tasks" %}

We all know what it's like to be given a vague job to do, or to receive a poor bug report. The GitHub community felt this pain so acutely that there was a somewhat [large outcry for GitHub to provide solutions to the situation](https://github.com/dear-github/dear-github). It's both annoying and a productivity sink having to chase up details that should of been provided from the outset, and while there exist a large number of templates for bug reports, I haven't seen anywhere near as many resources for writing tasks for your colleagues.

When learning about storytelling as a child I was introducted to [The Five Ws](https://en.wikipedia.org/wiki/Five_Ws). "Who, what, where, when, why", apart from being part of [Abbott and Costello's starting lineup](https://www.youtube.com/watch?v=kTcRRaXV-fg), is a useful technique for helping to remember what you as an author need to get across to the audience. But with software, sometimes we're not writing a task for a specific person, or to be done at a specific point in time, so specifying 'where' doesn't always make sense.

I'd argue that when writing a task the three things that are necessary are **Context**, a **Task Description** and a set of **Deliverables**.

## Context
Context is the _why_ of the change. It tells the person that is assigned the task what the thinking of the task author or team was at the time the task was created, and what led to the creation of the task. This is the start of the story, the first act, setting the scene for those that work on the task.

> After meeting with the UX consultant there were a number of recommendations made for our e-commerce product line. One recommendation was to decrease the friction in the new user signup workflow. As a large number of our new users initially have accounts in order to save and compare several different items one method of reducing friction for those new users would be to stop asking for so much information at signup time.

## Task Description
Hopefully all the tasks that you are writing or being assigned already have a good task description. This should explain _what_ actually needs to be done, as well as any extra considerations that need to be taken in to account by the future assignee.

> We should change the required information for new user account signup to be a valid email address and password. We should also change the purchase handling code to check that a user has all the necessary shipping and payment information to complete a purchase.

{% include captioned_gfycat_image.html gfycat="SelfreliantInfamousCanvasback" caption="Context and a good task description are so important the Asana homepage lists them as features of the product" %}

## Deliverables
As the final act of the story the deliverables will be _how_ we know we are finished and _how_ will we measure success. A lot of the time this is simply rolled in to the same paragraph as the task description, but I find it helpful to think of it as a separate part of the task. What is going to come out of the completion of this task? Is there some documentation required? What should that documentation cover? Are there any non-functional requirements that need to be addressed?

> This should result in modifications to the new user signup front-end and backend code, as well as new business logic in the purchase handling code to ensure all the information required to make a purchase is provided. Please also update the system documentation with information about the new account requirements and signup workflow.

## But Wait, There's More!
While the above-mentioned constructs will certainly get you on track to writing great tasks, it's worth keeping in mind the specifics of your environment. Would it be helpful for you to provide extra information for the person testing the deliverables? Is there anything the reviewer should pay particular attention to? Some of these extra details may only become available as the task is being completed, so it's important to be aware of your colleague's requirements, and to have a bit of empathy for them.

So what value do we gain from following a system like this? Well, for one, if you're in a large team _anybody_ should be able to pick up the task and run with it. All of this extra information will be greatly appreciated by those not intimately familiar with the change already, those unfamiliar with the code-base and potentially yourself if you don't get around to doing the task for a few months.
