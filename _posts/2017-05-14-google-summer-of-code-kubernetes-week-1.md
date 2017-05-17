---
layout: post
title: GSoC with Kubernetes - Week 1
description: My experience as a Google Summer of Code intern with Kubernetes (Cloud Native Computing Foundation). Week 1 - Community Bonding Period.
comments: true
keywords: google summer of code, community bonding, community bonding period, gsoc, soc, summer of code, nikhita raghunath, vjti, kubernetes, cncf, cloud native computing foundation, k8s, nikhita, week 1, experience, third party resources, tpr, tprs
---

# Getting in

In my last [post](https://nikhita.github.io/experience-gophercon-india), I mentioned about speaking at GopherCon India. It was a surreal experience and it introduced me to Kubernetes. I was aware of Kubernetes before (having used Docker) but didn't really take the leap to contributing to it. Attending the conference made me go "Damn, this sounds so cool. I am definitely looking at the contributing guide after I get back home!".

Luckily, the day I got back home was the day when organizations for Google Summer of Code were announced. I was **beyond enthralled** to see [CNCF](https://github.com/cncf/soc) on the list and started reading the documentation for Kubernetes right away. It took me about a week to get comfortable with k8s and the project, set up my development environment and understand the codebase. I solved a few issues for the pre-GSoC involvement, discussed and got my proposal reviewed from my mentor.

After a month long wait, contributions and exams, I finally got the result that I had been selected for Google Summer of Code this year! Last winter, I had applied for [Outreachy](https://wiki.gnome.org/Outreachy) and was going to be selected but couldn't join later due to timeline restrictions (Outreachy needed two months of winter vacations while I had just one month free). I was bummed to hear that and my thirst to get into GSoC strengthed even more. Receiving the GSoC result was one of the best moments of my life!   :smile:

# My project

Kubernetes comes with many built-in API objects. However, it also offers you the feature to extend the Kubernetes API using Third Party Resources (TPRs). TPRs are a very exciting and crucial part of Kubernetes since it offers one to create their own custom objects. You can think of TPRs as being much like the schema for a database table. Once you have created the table, you can then start storing rows in the table. Once created, TPRs can act as the data model behind custom controllers or automation programs.

The implementation to allow the creation of TPRs is present but the implementation has languished. There are multiple problems associated with it and one of my goals this summer is to work on these problems to drive them stable and to shower some love at TPRs! One of the main features I will be working on is implementing validation. If time permits, other features will also be added. You can read about the current situation of Third Party Resources [here](https://github.com/kubernetes/features/issues/95).

# The Community

Google lets students get comfortable with the community, their projects and the development environment initially. The student is not required to code right away. This period is to allow students to refine their project ideas so they can code without any hassle during the coding period. Hence, this period is called the Community Bonding Period. I really liked this approach. :heart:

My first week has been absolutely amazing! I had the **best** time working with my mentor - [Dr. Stefan Schimanski](https://github.com/sttts). Even when I did not know something, he explained with utmost patience without making me feel bad about not knowing it. Meanwhile, I was also encouraged to ask questions without hesitation. This gives a HUGE boost to us mentees while communicating with mentors. I am deeply thankful for his help.

My experience interacting with other community members has been positive too. I tweeted about my gsoc selection and was overwhelmed to recieve such a warm welcome from the community! Even while interacting on slack and github, everyone has been very friendly. The environment is very pleasant and I am having great fun working with such an awesome community! Kubernetes takes the cake for being the friendliest open source community ever!

<br>

<div align="center">
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Excited to work on <a href="https://twitter.com/kubernetesio">@kubernetesio</a> as my <a href="https://twitter.com/gsoc">@gsoc</a> project! 🎉 <a href="https://t.co/pir10SzTZe">https://t.co/pir10SzTZe</a></p>&mdash; Nikhita Raghunath (@TheNikhita) <a href="https://twitter.com/TheNikhita/status/860238784205606912">May 4, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

<br>

The CNCF community has been very engaging and hospitable too. After the selection, CNCF released a [blog post](https://www.cncf.io/blog/2017/05/04/cncf-brings-kubernetes-coredns-opentracing-prometheus-google-summer-code-2017/) on their website mentioning about us GSoC students and they were very friendly over email and slack as well. I feel very lucky to be part of CNCF. :)

# The Work

 * One of the main features I will be implementing for TPRs is validation. This week I started out with comparing two go json schema libraries that we could use for validation. I wrote benchmarks for the same and chose one of them after analyzing their strengths and weaknesses.

* I will soon be publishing a design proposal for validation. I researched a bit more about it, made notes and wrote down tricky questions that the project could face. There are still some open questions and I will be addressing them and coming up with the draft proposal next week.

* [David](https://github.com/deads2k) had been working on creating a stable base for TPRs (now it will probably be called Custom Resources). He even wrote a nice step-by-step approach on setting up the new kube-apiextensions-server which I transformed into a bash [script](https://github.com/nikhita/gsoc-meta-k8s/blob/master/notes/set-kube-apiextensions-server.sh) for easy access. ;)

* I began tinkering around with the new TPR code and started out writing integration tests for the same. The pull request can be seen [here](https://github.com/kubernetes/kubernetes/pull/45721) and the list of integration tests can be seen [here](https://github.com/kubernetes/kubernetes/issues/45511). I plan to add more integration tests, solve issues and help out with [migration](https://github.com/kubernetes/kubernetes/issues/45728) in the coming weeks.

I have been maintaining a google doc with daily updates which serves as a neat log of what I am working on. A major benefit is that I can take a step back and see the overall progress of my project. I have collated everything related to my GSoC project in one [meta repository](https://github.com/nikhita/gsoc-meta-k8s) on Github. If you are interested in knowing more about this project, please visit the repo for a better perspective on it. :)

# Conclusion

I don't intend to write such long blog posts about my weekly progress in the future (I will definitely write, but they will be short and sweet). These blog posts provide a rather detailed and personal overview of my experience. Instead if you are interested in knowing only about the progress, you can visit the repo to get summarized weekly reports!

When I started out with Kubernetes, I faced a lot of trouble getting a hang out of it. In the coming weeks, I also plan on writing a few blog posts for beginners. I believe that being a newbie myself, I can offer a better and a fresher perspective. So come back after a few weeks to read more!

I am having immense fun working with the Kubernetes team and I plan on contributing more and continuing to have more fun over the summer! :tada:




