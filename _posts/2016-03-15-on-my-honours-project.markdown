---
layout: post
title: "On My Honours Project"
tags:
categories:
date: 2016-03-15 10:45PM
cover: "glacier_point_jordan_mcqueen.jpg"
cover_artist: Jordan McQueen
cover_link: https://unsplash.com/photos/93g2k8D1Mi8
---

As an undergraduate engineering student at [the University of Newcastle](http://newcastle.edu.au/) I have to complete an honours project during my studies in order to receive my degree. Last year I managed to complete that project, and it was a very different type of project compared to what I'm used to. I've linked to the code repository and the report submission at the bottom of this blog post.

Typically the assignments that I've encountered throughout my undergraduate study have been very structured, well specified, lecture material supported affairs. Most mentions of requirements gathering have been from a purely theoretical point of view, and unfortunately often paired with out of date or simply misinformed views of enterprise. This is systemic of what I think is a much broader problem with the western education systems I've experienced, but I digress.

This honours project was quite the rude shock when I came to it and was given very little in the way of structure or guidelines. I was merely tasked with "Going off and researching, building and documenting a system and showing off all the neat software engineering practices that I'd learnt throughout my study". Admittedly, I am paraphrasing my own perception of the activity heavily here.


# Genesis
This was a surprisingly difficult part of the project. I struggled greatly to even settle on an idea of what I wanted to research. Towards the end of first semester I was supposed to be submitting an interim report, that mostly would be marked on my research in to my chosen topic, taking the form of a literature review, and some project planning documentation, in the form of development plans and a project timeline.

{% include quote.html content="This project will explore the facilitation of collaboration between multiple students around a single large multi-touch surface. There will be a focus on providing students with a means of working on their own and then sharing their work with other students, which I have termed the private workspace problem." author="Me, in my initial project specification, submitted in week three" %}

Wow, doesn't that just sound like a heap of fluff?

Three days before I submitted my interim report, the project suffered something of an identity crisis. All throughout the semester I had felt as though I was not completely sold on my chosen topic, but I had somewhat backed myself in to a corner by spending the entire semester researching collaborative multitouch environments in educational contexts.

This didn't leave me with many options for potential problem statements that I would be able to research before the deadline. In those last three days I spent a lot of time reworking the literature review, but those limited options and need to come up with a solution quickly really helped me to focus in on something that I felt was not only interesting, but could actually be completed within the next semester.


# The Thesis
I eventually settled on trying to determine a method of determining whether or not forcing people to collaborate was possible and what effect that would have on those individuals.

In order to test my thesis I built an application that could be operated in two modes, one which would force the participants to collaborate, and one which could be completed by an individual. This took the form of a basic puzzle game wherein participants would need to line up a number of coloured dots with some similarly coloured in the background.

## Forcing Collaboration
In the forced collaboration mode the dots would return to the center of the play area once the participants stopped touching them, thereby forcing the participants to keep both their hands on the table. As more and more dots were added to it became unreasonable for a single individual to complete the puzzle. The idea was to increase the likelihood that the individuals would communicate and work together to achieve their common goal. In the individually completable mode of the game the dots would just remain where they were last touched.

## Measuring Collaboration
In researching for this project I began to look at more formalised definitions of collaboration. It's quite easy to summarise and distill an individual's idea of what it means to collaborate, but the measurement of collaboration is somewhat less clear, as collaboration is an intangible concept. I settled on tracking a number of actions that users performed and classified them as collaborative actions, and similarly for non-collaborative actions.

When participants spoke to eachother, or were both completing the puzzle they were said to be collaborating, but if one participant disengaged from the activity in any way that collaboration was said to have ceased. I had recorded the sessions, and was able to go over the footage later in order to record whether the participants were collaborating or not to 1 second resolution. This allowed me to graph and compare the amount of collaboration between each mode and other participant groups.

{%include captioned_image.html image="group_collaboration_results.png" caption="A comparison of total time spent collaborating among the participant groups" %}

# Difficulties Faced
There were marks awarded for integrating the individual honours project with the year long group project for final year software engineering students. Given the problem we were attempting to solve in the group project I began by trying to solve my problem using similar technologies to those used in the group project, which unfortunately for me meant JavaScript.

I had never really dealt with JS before last year. And while having strong software development fundamentals will get you a long way with learning another language there is still a significant barrier to entry. Not being able to write idiomatic JavaScript left me open to hitting the sort of problems that a more experienced hand might easily be able to avoid. Heck, pretty much all of the debugging I did was using `console.log(...)`, which I'm sure is not how most JavaScript developers live their lives.

As with all student projects, the more that time constraints loomed the messier (and scarier) my code got. At one point I was returning a heap of HTML as a string from a function and then appending it to one of the pre-existing layers. Sure, that's actually still happening a little bit, but it's not as bad as it once was.

Even after the code itself was finished and I had completed the user studies I was faced with the prospect of trying to find some sort of quantitative result from the data I had collected. Statistics is one of those subjects that I've never really understood, and attempting to discover some meaning in either the Likert-like survey results I asked the participants to fill out and the collaboration data just reinforced how little I really understand about statistical analysis.


# Results
From what I could gather it is possible to force participants to collaborate, and when I did force them to collaborate the participants didn't have a negative reaction to the activity, which was one of my initial concerns.

As with anything like this it would be interesting to see if the results generalise to different demographics and different activities, as well as what other methods of forcing collaboration may exist.


# Code
I had some reservations about releasing the code for this. Partly because it is far from the nicest code I've ever written. I spent a bit of time while writing this blog post removing as much of the group project code from it as possible, since it doesn't really need to have all the dependencies that the rest of the project had. Anybody that has spent a reasonable amount of time dealing with JavaScript in a professional manner could probably tear this to shreds.

Alright, enough hedging against myself; [here's the source <i class="fa fa-github"></i>](http://github.com/Huddo121/Dots-Honours-Project.git).

I've set up the GitHub Pages branch for the project with the latest code, so you can [click here](http://huddo121.github.io/Dots-Honours-Project) to play with the application (best experienced with a friend on a large table or multitouch table).

And [here](/files/honours_thesis.pdf) is the final report submission that I made.
