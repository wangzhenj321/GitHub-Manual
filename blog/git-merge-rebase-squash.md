**Table of Contents**

[`git merge`](#git-merge)

[`git rebase`](#git-rebase)

[`git merge --squash`](#git-merge---squash)

[References](#references)

Suppose originally there were 3 commits, `A`, `B`, `C`:

![](../img/git-merge-rebase-squash/git_log.png?raw=true)

Then developer Dan created commit `D`, and developer Ed created commit `E`:

![](../img/git-merge-rebase-squash/git_two_commits_log.png?raw=true)

![](../img/git-merge-rebase-squash/git_log_of_DanBranch.png?raw=true)

![](../img/git-merge-rebase-squash/git_log_of_EdBranch.png?raw=true)

Obviously, this conflict should be resolved somehow. For this, there are 2 ways:

### `git merge`

![](../img/git-merge-rebase-squash/git_merge_log.png?raw=true)

![](../img/git-merge-rebase-squash/git_log_of_merge.png?raw=true)

Both commits `D` and `E` are still here, but we create merge commit `M` that inherits changes from both `D` and `E`. However, this creates diamond shape, which many people find very confusing.

### `git rebase`

![](../img/git-merge-rebase-squash/git_rebase_log.png?raw=true)

![](../img/git-merge-rebase-squash/git_log_of_rebase.png?raw=true)

We create commit `R`, which actual file content is identical to that of merge commit `M` above. But, we get rid of commit `E`, like it never existed (denoted by dots - vanishing line). Because of this obliteration, `E` should be local to developer Ed and should have never been pushed to any other repository. Advantage of rebase is that diamond shape is avoided, and history stays nice straight line - most developers love that!

### `git merge --squash`

```
git merge --squash newBranch
```
will produce a squashed commit on the destination branch, without marking any merge relationship. (Note: it does not produce a commit right away: you need an additional `git commit -m "squash branch"`)

This is useful if you want to throw away the source branch completely, going from
```
git checkout stable

      X                   stable
     /                   
a---b---c---d---e---f---g tmp
```
to
```
git merge --squash tmp
git commit -m "squash tmp"

      X-------------------G stable
     /                   
a---b---c---d---e---f---g tmp
```

## References
1. [What's the difference between 'git merge' and 'git rebase'?](https://stackoverflow.com/questions/16666089/whats-the-difference-between-git-merge-and-git-rebase)
2. [In git, what is the difference between merge --squash and rebase?](https://stackoverflow.com/questions/2427238/in-git-what-is-the-difference-between-merge-squash-and-rebase)
