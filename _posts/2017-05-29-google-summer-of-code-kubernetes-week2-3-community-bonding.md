---
layout: post
title: GSoC with Kubernetes - Week 2 and 3
description: My experience as a Google Summer of Code intern with Kubernetes (Cloud Native Computing Foundation). Week 2 and 3 - Community Bonding Period.
comments: true
keywords: google summer of code, community bonding, community bonding period, gsoc, soc, summer of code, nikhita raghunath, vjti, kubernetes, cncf, cloud native computing foundation, k8s, nikhita, week 1, experience, third party resources, tpr, tprs
tags:
- gsoc
---

This is an update of Week 2 and 3 for my Google Summer of Code project with Kubernetes (Cloud Native Computing Foundation). I ended up coding a lot more, talking to other community members and having even more fun. :smile:

## The Code Part

I mainly wrote a lot of integration tests and fixed bugs along the way for CRDs. Code freeze is up on June 1 so I'd like to get all integration tests by then (only a couple remaining!). So CRDs should be perfectly polished and ready by 1.7.

I also collated ideas related to the proposal and added a validation schema for Pod - will be working on the proposal more in the next week (after the code freeze).

* Added the following integration tests:
    - test for no namespace rejection
    - test for creating resources with same name and different namespace
    - test for checking if integers are preserved while decoding (originally a TPR regression)
    - test for self link of cluster scoped resources
    - test for name conflicts

* Created some more PRs/issues:
    - Add plural name for CustomResources example in [#45793](https://github.com/kubernetes/kubernetes/pull/45793)
    - Fixed the controller doc in [#621](https://github.com/kubernetes/community/pull/621)
    - Created an [issue](https://github.com/kubernetes/test-infra/issues/2787) on `kubernetes/test-infra` for a flake that was hitting all PRs. See [this](https://github.com/kubernetes/kubernetes/issues/45978) issue for further discussion.

## The Tale of CRD Deletion:
While writing the test for name conflicts, I hit a lot of bugs and it was interesting solving them!

It initially caused a panic ([stack trace](https://gist.github.com/nikhita/345c3629fc4a942b7c9ee5275dfeb74b)). This occurred because now we deleted from storage instead of the client (after this [PR](https://github.com/kubernetes/kubernetes/pull/46296)). This was racing the storage and causing a nil dereference. PR with fix: [#46430](https://github.com/kubernetes/kubernetes/pull/46430).

Did a rebase again but still did not work! Now I got:  `"reason": "InstanceDeletionFailed"` and `"message": "could not list instances: unable to find a custom resource client for noxus.mygroup.example.com"`. The problem turned out to be that the storage map was only filled if a CR (not the CRD!) was accessed via some CRUD request. So this worked only if you created CRs before the CRD deletion. PR with fix: [#46501](https://github.com/kubernetes/kubernetes/pull/46501). 

Also fixed the naming controller so that when a resource is deleted, other resources in the same group are added to the queue. This is necessary since the deleted CRD can free names. Added a `requeueAllOtherGroupCRDs` function for the above. Had a little trouble making the synchronization was right. I was using `time.Sleep` before which looked very wrong. Tried polling later, then thought that polling was in fact not needed at all! Finally added in the right place (in `apierrors.NotFound(err)`) and got it working! :boom:

## The Community Bonding Part

I talked to David (who is working on CRDs a lot) about the project/CRDs and he was very helpful! I had not spoked to him before so this was a nice community bonding exercise.

I also helped a few folks on Slack and answered their questions. Lots of people reached out to be in these two weeks asking me how they could contribute to Kubernetes. It was exciting seeing the sudden interest! I think most of them faced the issue of not being able to find a beginner-friendly task. I pointed them to a few easy issues but hope to come up with a solution to that!

I even did my first small code review. That felt great because I never thought I could ever be so confident about a codebase to do a review of others' code. :grinning:

## Conclusion

I am really enjoying working with the Kubernetes community. Everyone is very friendly and I look forward to Mondays now (yes, you read that right!). 

PS: Had some Twitter fun this week -

<br>

<div align="center">
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/TheNikhita">@TheNikhita</a> Thanks for your work so far <a href="https://twitter.com/TheNikhita">@TheNikhita</a>! You fixed a bug that we hit in Kubernetes and is getting backported to the next 1.6.x branch 👍👍👍</p>&mdash; Brandon Philips (@BrandonPhilips) <a href="https://twitter.com/BrandonPhilips/status/867820077063602176">May 25, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<br>
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Love seeing <a href="https://twitter.com/hashtag/gsoc?src=hash">#gsoc</a> interns making impact in <a href="https://twitter.com/kubernetesio">@kubernetesio</a> <a href="https://t.co/zSPxOZIZx7">https://t.co/zSPxOZIZx7</a> <a href="https://t.co/rj9ooTHFOo">https://t.co/rj9ooTHFOo</a></p>&mdash; Brandon Philips (@BrandonPhilips) <a href="https://twitter.com/BrandonPhilips/status/867821071872909312">May 25, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>


<br>


