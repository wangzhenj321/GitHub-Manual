## Question
I recently forked a project and applied several fixes. I then created a pull request which was then accepted.

A few days later another change was made by another contributor. So my fork doesn't contain that change... How can I get that change into my fork?

Do I need to delete and re-create my fork when I have further changes to contribute? Or is there an update button?

## Answer
In your local clone of your forked repository, you can add the original GitHub repository as a "remote". ("Remotes" are like nicknames for the URLs of repositories - origin is one, for example.) Then you can fetch all the branches from that upstream repository, and rebase your work to continue working on the upstream version. In terms of commands that might look like:
```
// Add the remote, call it "upstream"
$ git remote add upstream https://github.com/whoever/whatever.git

// Fetch all the branches of that remote into remote-tracking branches,
// such as upstream/master
$ git fetch upstream

// Make sure that you're on your master branch
$ git checkout master

// Rewrite your master branch so that any commits of yours that aren't already
// in upstream/master are replayed on top of that other branch
$ git rebase upstream/master
```
If you don't want to rewrite the history of your master branch, (for example because other people may have cloned it) then you should replace the last command with git merge upstream/master. However, for making further pull requests that are as clean as possible, it's probably better to rebase.

***
If you've rebased your branch onto upstream/master you may need to force the push in order to push it to your own forked repository on GitHub. You'd do that with:
```
$ git push -f origin master
```
You only need to use the -f the first time after you've rebased. Usually, the command `git push` refuses to update a remote ref (origin) that is not an ancestor of the local ref (master) used to overwrite it. The flag -f disables these checks, and can cause the remote repository (origin) to lose commits, and makes the remote repository (origin) to be totally replaced by the local repository (master); use it with care. The reason why we say "you only need to use the -f the first time" is that we suppose the master branch will not be used for development, so the remote refs (origin) will always be the ancestor of the local refs (master).
***

## References
1. [How do I update a GitHub forked repository?](https://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository)