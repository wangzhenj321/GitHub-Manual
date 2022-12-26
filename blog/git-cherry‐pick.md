**Table of Contents**

**[Part 1](#part-1)**

- [Question](#question)

- [Answer](#answer)

- [References](#references)

**[Part 2](#part-2)**

- [Rebasing and Cherry-Picking Workflows](#rebasing-and-cherry-picking-workflows)

- [`git cherry-pick`](#git-cherry-pick)

    - [Description](#description)
    
    - [Synopsis](#synopsis)
    
    - [Options](#options)
    
    - [Examples](#examples)

# Part 1

## Question
I have `BranchA` which is 113 commits ahead of `BranchB`.

But I only want the last 10 or so commits from `BranchA` merged into `BranchB`.

Is there a way to do this?

## Answer
The `git cherry-pick <commit>` command allows you to take a single commit (from whatever branch) and, essentially, rebase it in your working branch.

[Chapter 5 of the Pro Git book explains it better than I can](https://git-scm.com/book/en/v2/Distributed-Git-Maintaining-a-Project#Integrating-Contributed-Work), complete with diagrams and such; look for the section entitled "Rebasing and Cherry Picking Workflows". ([The chapter on Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) is also good reading.)

Lastly, there are some [good comments on the cherry-picking vs merging vs rebasing in another SO question](https://stackoverflow.com/questions/1241720/git-cherry-pick-vs-merge-workflow).

## References
1. [How do I merge a specific commit from one branch into another in Git?](https://stackoverflow.com/questions/6372044/how-do-i-merge-a-specific-commit-from-one-branch-into-another-in-git)
2. [How to merge a specific commit in Git](https://stackoverflow.com/questions/881092/how-to-merge-a-specific-commit-in-git)

# Part 2

## Rebasing and Cherry-Picking Workflows

Other maintainers prefer to rebase or cherry-pick contributed work on top of their master branch, rather than merging it in, to keep a mostly linear history. When you have work in a topic branch and have determined that you want to integrate it, you move to that branch and run the rebase command to rebuild the changes on top of your current `master` (or `develop`, and so on) branch. If that works well, you can fast-forward your master branch, and you’ll end up with a linear project history.

The other way to move introduced work from one branch to another is to cherry-pick it. **A cherry-pick in Git is like a rebase for a single commit. It takes the patch that was introduced in a commit and tries to reapply it on the branch you’re currently on.** This is useful if you have a number of commits on a topic branch and you want to integrate only one of them, or if you only have one commit on a topic branch and you’d prefer to cherry-pick it rather than run rebase. For example, suppose you have a project that looks like this:

![](../img/git-cherry-pick/cherry-pick-1.png?raw=true)

If you want to pull commit e43a6 into your master branch, you can run

```
$ git cherry-pick e43a6
Finished one cherry-pick.
[master]: created a0a41a9: "More friendly message when locking the index fails."
 3 files changed, 17 insertions(+), 3 deletions(-)
 ```
 
This pulls the same change introduced in e43a6, but ***you get a new commit SHA-1 value***, because the date applied is different. Now your history looks like this:

![](../img/git-cherry-pick/cherry-pick-2.png?raw=true)

Now you can remove your topic branch and drop the commits you didn’t want to pull in.

## `git cherry-pick`

### Description

Given one or more existing commits, apply the change each one introduces, recording a new commit for each. **This requires your working tree to be clean (no modifications from the HEAD commit).**

### Synopsis

- `git cherry-pick [--edit] [-n] [-m parent-number] [-s] [-x] [--ff] [-S[<keyid>]] <commit>...`

- `git cherry-pick --continue`

- `git cherry-pick --abort`

### Options

- `<commit>...`

    Commits to cherry-pick.

- `-e, --edit`

    With this option, `git cherry-pick` will let you edit the commit message prior to committing.

- `-m parent-number, --mainline parent-number`

    Usually you cannot cherry-pick a merge because you do not know which side of the merge should be considered the mainline. This option specifies the parent number (starting from 1) of the mainline and allows cherry-pick to replay the change relative to the specified parent.
    
    A good example about how to select the parent number: https://qiita.com/takc923/items/8e2d87d692f840b14464.

- `-n, --no-commit`

    Usually the command automatically creates a sequence of commits. This flag applies the changes necessary to cherry-pick each named commit to your working tree and the index, without making any commit. In addition, when this option is used, your index does not have to match the HEAD commit. The cherry-pick is done against the beginning state of your index.

    This is useful when cherry-picking more than one commits' effect to your index in a row.

### Examples

1. `git cherry-pick master`

    Apply the change introduced by the commit at the tip of the master branch and create a new commit with this change.

2. `git cherry-pick ..master`, `git cherry-pick ^HEAD master`

    Apply the changes introduced by all commits that are ancestors of master but not of HEAD to produce new commits.

3. `git cherry-pick master~4 master~2`

    Apply the changes introduced by the fifth and third last commits pointed to by master and create 2 new commits with these changes.
