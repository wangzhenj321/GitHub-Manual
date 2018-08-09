### local branch

You can delete a merged local branch with:
```
git branch -d branchname
```
If it's not merged, use:
```
git branch -D branchname
```

### remote branch

To delete it from the remote repo use:
```
git push --delete origin branchname
```
With this command, the corresponding remote-tracking branch will also be deleted.

Or you can delete the remote branch with the delete button in the list of branch on your GitHub.

### remote-tracking branch

Once you delete the branch from the remote, you can prune to get rid of remote-tracking branches with:
```
git remote prune origin
```
or fetch from your remote repo, and remove remote-tracking branches from your local repo that are no longer on the remote, with:
```
git fetch -p origin
```
or prune individual remote-tracking branches, as the other answer suggests, with:
```
git branch -dr origin/branchname
```

> You can see a list of branches that were already merged, with:
> ```
> git branch -a --merged
> ```

## References
1. [How can I delete all Git branches which have been merged?](https://stackoverflow.com/questions/6127328/how-can-i-delete-all-git-branches-which-have-been-merged)
2. [Clean up unused git branches](https://ardalis.com/clean-up-unused-git-branches)
