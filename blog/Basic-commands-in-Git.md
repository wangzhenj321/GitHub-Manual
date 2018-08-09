#### Table of Contents

| [gc](#gc) | [help](#help) | [init](#init) | [log](#log) | [status](#status) | [reset](#reset) | [add](#add) | [commit](#commit) | [clone](#clone) | [remote](#remote) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [**fetch**](#fetch) | [**pull**](#pull) | [**push**](#push) | [**diff**](#diff) | [**show**](#show) | [**checkout**](#checkout) | [**branch**](#branch) | [**merge**](#merge) | [**tag**](#tag) | [**clean**](#clean) |
| [**stash**](#stash) |

### gc

- `git gc`

### help

- `git help {-a | -g}`

    list available sub-commands and some concept guides

- `git help {command | concept}`

    read about a specific sub-command or concept

### init

- `git init`

    initialize a repository in an existing directory

### log

- `git log`

    show the committed logs

- `git log --stat`

    `--stat` gives some statistics which files have changed in each commit

- `git log --graph --oneline {branch name 1} {branch name 2} ...`

    see the visual representation of the commit history

- `git log -n {number}`

    `-n` flag means that git log will only show that number of commits

- `git log --graph`

    Draw a text-based graphical representation of the commit history on the left hand side of the output. This may cause extra lines to be printed in between commits, in order for the graph history to be drawn properly.

- `git log --pretty[=<format>]`

    Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, short, medium, full, fuller, email, raw, format:<string> and tformat:<string>.

- `git log --abbrev-commit`

    Instead of showing the full 40-byte hexadecimal commit object name, show only a partial prefix.

- `git log --oneline`

    This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

- `git log --decorate[=short|full|no]`

    Print out the ref names of any commits that are shown. If short is specified, the ref name prefixes refs/heads/, refs/tags/ and refs/remotes/ will not be printed. If full is specified, the full ref name (including prefix) will be printed. The default option is short.

### status

- `git status`

    check the status of your files

- `git status -uno`

    Show no untracked files.

- `git status -unormal`

    Shows untracked files and directories.

- `git status -uall`

    When `-u` option is not used, untracked files and directories are shown (i.e. the same as specifying normal), to help you avoid forgetting to add newly created files. Also shows individual files in untracked directories.

### reset

- `git reset {filename in the staging area}`

    undo the “git add” : put the file in the staging area back to the working directory

- `git reset --hard`

    Undo the changing operations in the working directory and the staging area. Any changes to tracked files in the working tree since <commit> are discarded.

- `git reset HEAD~3`

    Rewind the master branch to get rid of those three commits, and keep the changes of those three commits in the working directory. If you want to remove these changes, you can use previous option '--hard'.

### add

- `git add {filename in the working directory}`

    add the file from the working directory into the staging area

### commit

- `git commit [-m “Commit message”]`

    commit the current changes in the staging area

### clone

- `git clone {url} [rename directory]`

    clone the whole repository from the url

### remote

- `git remote`

    view remotes

- `git remote add {reference name of remote repository | origin} {url}`

    (create an empty repository on Github first) add the repository on Github as a remote

- `git remote -v`

    `-v` means that git remote will output more information

### fetch

- `git fetch {reference name of remote repository | origin}`

    update all of the local copies of every branch for the remote (`git pull = git fetch + git merge`)

### pull

- `git pull {reference name of remote repository | origin} {local branch name}`

    pull the changes you made on Github into your local repository

### push

- `git push {reference name of remote repository | origin} {local branch name}`

    send local changes to the remote

### diff

- `git diff `

    compare the working directory with the staging area

- `git diff --staged`

    compare the staging area with the latest committed

- `git diff {commit ID 1} {commit ID 2}`

    compare the commit ID 1 with the commit ID 2

### show

- `git show {commit ID}`

    show the diff between this commit and its parent without actually knowing what the parent was

### checkout

- `git checkout {commit ID}`

    switch to the commit point of “commit ID"

- `git checkout {branch name}`

    switch to the branch of “branch name"

- `git checkout -- {file name}`

    discard changes of "file name" in working directory

### branch

- `git branch`

    list the branches

- `git branch -a`

    list both remote-tracking branches and local branches

- `git branch {branch name}`

    create the new branch, named of “branch name”

- `git branch -m {old name} {new name}`

    rename a branch while pointed to any branch

- `git branch -m {new name}`

    rename the current branch

- `git branch -d {branch name}`

    only delete the label of branch, not delete the commits in the branch

### merge

- `git merge {branch name 1} {branch name 2} ...`

    `git checkout master` to make sure on branch master, and let the master branch to update and point to the merged version

---

**`git merge` will also include the currently checked-out branch in the merged version.** So if you have branch1 checked out, and you run `git merge branch2 branch3`, the merged version will combine branch1 as well as branch2 and branch3. That’s because the branch1 label will update after you make the merge commit, so it’s unlikely that you didn’t want the changes from branch1 included in the merge. For this reason, you should always checkout one of the two branches you’re planning on merging before doing the merge. Which one you should check out depends on which branch label you want to point to the new commit.

Since the checked-out branch is always included in the merge, you may have guessed that when you are merging two branches, you don't need to specify both of them as arguments to `git merge` on the command line. If you want to merge branch2 into branch1, you can simply `git checkout branch1` and then type `git merge branch2`. The only reason to type `git merge branch1 branch2` is if it helps you keep better mental track of which branches you are merging. 

Also, since the two branches are merged, the order in which they are typed into the command line does not matter. The key is to remember that `git merge` always merges all the specified branches into the currently checked out branch, creating a new commit for that branch.

---

### tag

- `git tag`

    list the tags

- `git tag {tag name}`

    create a tag on the latest commit

- `git tag {tag name} {commit ID}`

    create a tag on the “commit ID”

- `git show {tag name}`

    show the detail information of a tag

- `git tag -d {tag name}`

    delete the local tag

- `git push origin {tag name}`

    push the tag to origin

- `git push origin --tags`

    push all the tags to origin

- `git tag -d {tag name}`

    delete the remote tag on origin

- `git tag -a {tag name} -m {“tag message”} {commit ID}`

    `-a`: specify the tag name; `-m`: specify the tag message

### clean

[git clean](git-clean.md)

- `git clean`

    remove untracked files from the working tree

### stash

- `git stash save`

    Save your local modifications to a new stash entry and roll them back to HEAD (in the working tree and in the index). The <message> part is optional and gives the description along with the stashed state.

- `git stash list`

    List the stash entries that you currently have.

- `git stash pop`

    Remove a single stashed state from the stash list and apply it on top of the current working tree state, i.e., do the inverse operation of `git stash save`. The working directory must match the index.

- `git stash apply`

    Like pop, but do not remove the state from the stash list.

- `git stash clear`

    Remove all the stash entries.
