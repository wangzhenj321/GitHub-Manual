#### Table of Contents

| [gc](#gc) | [init](#init) | [reset](#reset) | [add](#add) | [commit](#commit) | [clone](#clone) | [**rm**](#rm) | [**fetch**](#fetch) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| [**pull**](#pull) | [**push**](#push) | [**checkout**](#checkout) | [**branch**](#branch) | [**merge**](#merge) | [**tag**](#tag) | [**revert**](#revert) |

### gc

- `git gc`

### init

- `git init`

    initialize a repository in an existing directory

### reset

> The \<tree-ish\>/\<commit\> defaults to HEAD in all forms.

- `git reset [<tree-ish>] [--] <paths>…`

    This form resets the index entries for all \<paths\> to their state at \<tree-ish\>. (It does not affect the working tree or the current branch.)

    This means that `git reset <paths>` is the opposite of `git add <paths>`.

    **Examples**
    
    - `git reset -- {filename in the staging area}`
    
        undo the `add`
        
        > `--` This option can be used to separate command-line options from the list of files, (useful when filenames might be mistaken for command-line options).

- `git reset [<mode>] [<commit>]`

    This form resets the current branch head to \<commit\> and possibly updates the index (resetting it to the tree of \<commit\>) and the working tree depending on \<mode\>. If \<mode\> is omitted, defaults to "--mixed". "--mixed" resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.

    **Examples**
    
    - `git reset --hard`
    
        Undo the changing operations in the working directory and the staging area. Any changes to tracked files in the working tree since \<commit\> are discarded.

    - `git reset HEAD~3`
    
        Rewind the master branch to get rid of those **three** commits, and keep the changes of those three commits in the working directory. If you want to remove these changes, you can use the above option '--hard'.

### add

- `git add {filename in the working directory}`

    This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit. 
    
    **The "index" holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit.** Thus after making any changes to the working tree, and before running the commit command, you must use the `add` command to add any new or modified files to the index.

    This command can be performed multiple times before a commit. It only adds the content of the specified file(s) at the time the add command is run; if you want subsequent changes included in the next commit, then you must run `git add` again to add the new content to the index.

### commit

- `git commit [-m “Commit message”]`

    commit the current changes in the staging area

### clone

- `git clone {url} [rename directory]`

    clone the whole repository from the url

---

Git has a number of different transfer protocols you can use. The previous example uses the https:// protocol, but you may also see git:// or user@server:path/to/repo.git, which uses the SSH transfer protocol.

---

### fetch

- `git fetch {reference name of remote repository | origin}`

    update all of the local copies of every branch for the remote (`git pull = git fetch + git merge`)

### pull

- `git pull {reference name of remote repository | origin} {local branch name}`

    pull the changes you made on Github into your local repository

### push

- `git push {reference name of remote repository | origin} {local branch name}`

    send local changes to the remote

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

### revert

- `git revert {commit}`

    Commits to revert.

- `git revert -n {commit}`

    Usually the command automatically creates some commits with commit log messages stating which commits were reverted. This flag applies the changes necessary to revert the named commits to your working tree and the index, but does not make the commits. In addition, when this option is used, your index does not have to match the HEAD commit. The revert is done against the beginning state of your index.

- `git revert HEAD~3`

    Revert the changes specified by the ***fourth*** last commit in HEAD and create a new commit with the reverted changes.

- `git revert -n master~5..master~2`

    Revert the changes done by commits from the ***fifth*** last commit in master (included) to the ***third*** last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index.

### rm

- `git rm [--cached] [--] <file>…`

    If you just use `rm`, you will need to follow it up with `git add <fileRemoved>`. `git rm` does this in one step.

    You can also use `git rm --cached` which will remove the file from the index (staging it for deletion on the next commit), but keep your copy in the local file system.
