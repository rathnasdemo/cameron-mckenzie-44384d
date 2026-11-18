---
schemaId: urn:gala:schema:content-frontmatter:2.0.0
schemaVersion: 2.0.0
id: 01a1f05c-92c4-7bcf-a48c-cf472e09bb07
kind: article
title: Resolve GitHub Merge Conflicts
description: I show how to create a GitHub merge conflict on purpose and then resolve it with the GitHub web editor, from the pull request through to confirming the merge worked.
language: en-US
authors:
- 01a1f061-2b8f-7bbd-aa81-388605f00509
tags:
- github
- git
- merge-conflicts
- pull-requests
- devops
status: published
createdAt: '2021-10-06T12:00:00.000Z'
publishedAt: '2021-10-06T12:00:00.000Z'
slug: resolve-github-merge-conflicts
hero:
  path: assets/content-resolve-github-merge-conflicts-hero.jpg
  alt: Thumbnail of the video "Resolve GitHub Merge Conflicts"
  role: informative
redirects: []
extensions: {}
---
*Adapted from the video [Resolve GitHub Merge Conflicts](https://www.youtube.com/watch?v=mOJazBNrG-c)*

> **TL;DR:** A merge conflict happens when two different branches edit the same file. To demonstrate, I create a feature branch from master, edit alpha.html on both branches, and open a pull request, which GitHub flags as unable to merge automatically. I then use the web editor to rewrite the conflicting code so it works together, mark it as resolved, commit the merge, and merge the pull request. Finally I check that both branches contain the merged code. The best fix, though, is not to have a conflict at all.

I'm Cameron McKenzie, editor-in-chief at theserverside.com, and I want to talk about merge conflicts in GitHub and how to use the GitHub IDE to fix them.

To show you how to resolve a GitHub merge conflict, you first have to create one, and that's fairly easy to do. A merge conflict happens when two different branches edit the same file.

## Creating a merge conflict

*[Watch from 0:23](https://www.youtube.com/watch?v=mOJazBNrG-c&t=23s)*

I've got an alpha.html file on the master branch, and there's nothing in it. I create a new branch called feature based on the master branch, so both branches now have this alpha file. Then I edit it on the feature branch, adding "hello feature branch world".

Now the alpha file on the feature branch is not the same as on the master branch. If I merged here, there would be no conflict, because the alpha file on the master branch hasn't changed. So let's poison this environment: I edit the file on the master branch too and write "goodbye world". We should really be in the main branch, but master is what I've got, so I'm sticking with it.

Now alpha.html has been updated in the master branch and on the feature branch, and Git has no idea how to merge the two together. But we're going to ask it to.

## Opening the pull request

*[Watch from 1:29](https://www.youtube.com/watch?v=mOJazBNrG-c&t=89s)*

I click on pull request and create a new pull request that merges feature into the master branch. Notice it barks right away: it cannot automatically merge into this branch. I click create pull request anyway, with a little comment in there that this needs to be fixed.

That's what you do if two people are working on the same file at the same time: you shout at them. The best way to fix a merge conflict is not to have a GitHub merge conflict at all.

## Resolving the conflict in the web editor

*[Watch from 2:12](https://www.youtube.com/watch?v=mOJazBNrG-c&t=132s)*

The page says this branch has conflicts which must be resolved, and to use the web editor or the command line. We'll use the web editor and do all of this in GitHub. This is all the help GitHub is going to give you: it says this is what's on the feature branch, that's what's on the master branch, and it has no way to figure out what you want to do, so you have to fix it.

In real life this would be Java code, with two people having written code in the same method. You're going to have to delete some code, add some code in, then make sure it compiles and passes tests. Again, the best way to resolve a merge failure is to not have them at all.

Here I just delete all of that and write "hello goodbye from the merge feature and master". That's all you can do: figure out how the code written by two people should work together, update it, compile it, pass your tests, and mark it as resolved. Then you commit the merge.

## Merging the pull request

*[Watch from 3:23](https://www.youtube.com/watch?v=mOJazBNrG-c&t=203s)*

Once the merge has been committed, the page may be out of date, so I reload it. You get to a page asking if you're ready to merge this pull request, since you created a new commit. I say yes: merge the pull request, then confirm the merge.

## Checking that it worked

*[Watch from 3:52](https://www.youtube.com/watch?v=mOJazBNrG-c&t=232s)*

Back in the GitHub merge examples there are no more pull requests, because that was resolved. On the master branch, alpha has the merged code on it. On the feature branch, alpha has the merged code as well. That's how you know the merge was successful.

And there you go, that's how you fix GitHub merge conflicts. If you enjoyed that tutorial, head over to theserverside.com, where we have lots of great tutorials on Git, GitHub and various devops tools. If you're interested in my personal analytics, you can follow me on Twitter at cameroncnc, and please subscribe on YouTube.

*[Watch the full video on YouTube](https://www.youtube.com/watch?v=mOJazBNrG-c)*
