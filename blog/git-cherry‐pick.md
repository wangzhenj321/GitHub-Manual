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

Other maintainers prefer to rebase or cherry-pick contributed work on top of their master branch, rather than merging it in, to keep a mostly linear history. When you have work in a topic branch and have determined that you want to integrate it, you move to that branch and run the rebase command to rebuild the changes on top of your current `master` (or `develop`, and so on) branch. If that works well, you can fast-forward your master branch, and you’ll end up with a linear project history.

The other way to move introduced work from one branch to another is to cherry-pick it. A cherry-pick in Git is like a rebase for a single commit. It takes the patch that was introduced in a commit and tries to reapply it on the branch you’re currently on. This is useful if you have a number of commits on a topic branch and you want to integrate only one of them, or if you only have one commit on a topic branch and you’d prefer to cherry-pick it rather than run rebase. For example, suppose you have a project that looks like this:

![](../img/git-cherry‐pick/cherry-pick-1.png?raw=true)

If you want to pull commit e43a6 into your master branch, you can run

```
$ git cherry-pick e43a6
Finished one cherry-pick.
[master]: created a0a41a9: "More friendly message when locking the index fails."
 3 files changed, 17 insertions(+), 3 deletions(-)
 ```
 
This pulls the same change introduced in e43a6, but you get a new commit SHA-1 value, because the date applied is different. Now your history looks like this:

![](../img/git-cherry‐pick/cherry-pick-2.png?raw=true)

Now you can remove your topic branch and drop the commits you didn’t want to pull in.
