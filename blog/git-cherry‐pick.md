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