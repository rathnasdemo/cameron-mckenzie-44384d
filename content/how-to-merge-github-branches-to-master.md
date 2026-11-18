---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1f05c-8fc2-7d8a-93fa-753196551e35
kind: article
title: How to Merge GitHub Branches to Master
description: I walk through merging a feature branch into master on GitHub with a pull request, then show how to resolve a merge conflict from a hotfix branch using the web editor.
language: en-US
authors:
- 01a1f061-2b8f-7bbd-aa81-388605f00509
tags:
- github
- git
- branches
- merge-conflicts
- pull-requests
status: published
createdAt: '2022-06-06T12:00:01.000Z'
publishedAt: '2022-06-06T12:00:01.000Z'
slug: how-to-merge-github-branches-to-master
hero:
  path: assets/content-how-to-merge-github-branches-to-master-hero.jpg
  alt: Thumbnail of the video "How to Merge GitHub Branches to Master"
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [How to Merge GitHub Branches to Master](https://www.youtube.com/watch?v=5g37NElQnCQ)*

> **TL;DR:** Merging branches in GitHub comes down to a pull request. I start with a development feature branch that only adds a beta.html file, so GitHub reports no conflicts and I confirm the merge into master. Then I merge a hotfix branch that changed the same alpha file as master, which creates a conflict. GitHub shows the code from each branch and asks what to keep, so I combine them in the web editor, mark the file as resolved, commit the merge and confirm it. The result is a master and hotfix branch that match.

I wanted to talk about GitHub, and specifically about branches and how you can merge them in GitHub.

My repository for this is called git merge examples, and it has three different branches. The master branch starts out with an alpha file that has nothing in it. I want to merge in a development feature branch, which just adds an extra file, beta.html. Finally I'm going to merge in a hotfix branch, which may cause a little problem because we may have a merge conflict. So I'll show you how to do a merge with a conflict as well.

## Merging the feature branch into master

*[Watch from 0:44](https://www.youtube.com/watch?v=5g37NElQnCQ&t=44s)*

First, the basic scenario: I want to merge the development feature branch, with its beta.html file, into master. I head to the master branch, which only has one file right now, and issue a new pull request, saying I want to pull the development feature branch into master.

After I click create pull request, GitHub tells me this branch has no conflicts with the base branch and asks if I want to do the merge. I confirm the merge, and that pull request successfully merges the feature development branch into the main branch. Going back to the master branch, we now see both the alpha file and the beta file. We've taken a development feature branch and merged it into master using GitHub.

## Creating a merge conflict

*[Watch from 2:01](https://www.youtube.com/watch?v=5g37NElQnCQ&t=121s)*

Now I'm going to do something a little different. I add some content to the alpha.html file and commit it, so this is now a commit on the master branch.

The problem is that when the hotfix branch was created, somebody also made changes to the alpha file. In the hotfix branch the code says goodbye world from hotfix, and in the master branch it says added some content to create a merge conflict. What do you think will happen if we try to merge these branches?

I create a pull request to pull from the hotfix branch into master. GitHub says it can't automatically merge this, because there is a merge conflict. I don't have a care in the world, so I create the pull request anyway and say I don't care, you fix it. Unfortunately, you is me.

## Resolving the conflict

*[Watch from 3:16](https://www.youtube.com/watch?v=5g37NElQnCQ&t=196s)*

GitHub says this branch has conflicts that must be resolved. We can use a web editor or the command line. I'm using the web editor, although you could pull down to your local file system and use the command line. Either way, this is what a conflict looks like: one part tells you the code in the hotfix branch, another tells you the code in the master branch, and it asks what you want to keep or how you want to bring them together.

The tool has no idea what to do with a conflict. Developers shouldn't be working on the same file at the same time, and when they do, these conflicts occur. If you were writing some HTML code or some Java code, you'd have to not only do the merge but also make sure the code compiles and passes any unit tests.

Here, I write hello goodbye combined for a merge. I mark the file as resolved and commit the merge. Now GitHub says everything is okay because we have resolved the conflict, and I confirm the merge.

## Checking the result

*[Watch from 4:43](https://www.youtube.com/watch?v=5g37NElQnCQ&t=283s)*

Back in git merge examples, I look at the master branch and open alpha.html. It has the content for the merge we just did, the code we wrote to merge the two branches together. On the hotfix branch, alpha also has hello goodbye combined for a merge in it. So the hotfix branch and the master branch are now merged together on GitHub, and that's how easy it is to merge git branches in GitHub.

If you enjoyed this tutorial, head over to theserverside.com, where I have lots of tutorials on Git, GitHub, DevOps tools and enterprise software development in general. If you're interested in my personal antics, you can follow me on Twitter at cameronmcnz, and please subscribe on YouTube.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=5g37NElQnCQ)*
