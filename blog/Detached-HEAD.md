## What's detached HEAD?

**HEAD normally refers to a named branch (e.g. master). Meanwhile, each branch refers to a specific commit.** Let's look at a repo with three commits, one of them tagged, and with branch master checked out:
> 
                      HEAD (refers to branch 'master')
                       |
                       v
           a---b---c  branch 'master' (refers to commit 'c')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

When a commit is created in this state, the branch is updated to refer to the new commit. Specifically, git commit creates a new commit d, whose parent is commit c, and then updates branch master to refer to new commit d. HEAD still refers to branch master and so indirectly now refers to commit d:
```
$ edit; git add; git commit
```
>
                          HEAD (refers to branch 'master')
                           |
                           v
           a---b---c---d  branch 'master' (refers to commit 'd')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

It is sometimes useful to be able to checkout a commit that is not at the tip of any named branch, or even to create a new commit that is not referenced by a named branch. Let's look at what happens when we checkout commit b (here we show two ways this may be done):
```
$ git checkout v2.0  # or

$ git checkout master^^
```
>
              HEAD (refers to commit 'b')
               |
               v
           a---b---c---d  branch 'master' (refers to commit 'd')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

**Notice that regardless of which checkout command we use, HEAD now refers directly to commit b. This is known as being in detached HEAD state. It means simply that HEAD refers to a specific commit, as opposed to referring to a named branch.** Let's see what happens when we create a commit:
```
$ edit; git add; git commit
```
>
                HEAD (refers to commit 'e')
                 |
                 v
                 e
                /
           a---b---c---d  branch 'master' (refers to commit 'd')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

There is now a new commit e, but it is referenced only by HEAD. We can of course add yet another commit in this state:
```
$ edit; git add; git commit
```
>
                    HEAD (refers to commit 'f')
                     |
                     v
                 e---f
                /
           a---b---c---d  branch 'master' (refers to commit 'd')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

In fact, we can perform all the normal Git operations. But, let's look at what happens when we then checkout master:
```
$ git checkout master
```
>
                          HEAD (refers to branch 'master')
                 e---f     |
                /          v
           a---b---c---d  branch 'master' (refers to commit 'd')
               ^
               |
             tag 'v2.0' (refers to commit 'b')

It is important to realize that at this point nothing refers to commit f. Eventually commit f (and by extension commit e) will be deleted by the routine Git garbage collection process, unless we create a reference before that happens. **If we have not yet moved away from commit f, any of these will create a reference to it:**
```
$ git checkout -b foo   (1)

$ git branch foo        (2)

$ git tag foo           (3)
```
1. creates a new branch foo, which refers to commit f, and then updates HEAD to refer to branch foo. In other words, we'll no longer be in detached HEAD state after this command.
2. similarly creates a new branch foo, which refers to commit f, but leaves HEAD detached.
3. creates a new tag foo, which refers to commit f, leaving HEAD detached.

**If we have moved away from commit f, then we must first recover its object name (typically by using git reflog), and then we can create a reference to it.** For example, to see the last two commits to which HEAD referred, we can use either of these commands:
```
$ git reflog -2 HEAD # or

$ git log -g -2 HEAD
```

## References
1. [git checkout - Detached HEAD](https://git-scm.com/docs/git-checkout#_detached_head)
