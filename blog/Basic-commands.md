#### Table of Contents

| [gc](#gc) | [init](#init) | [commit](#commit) | [clone](#clone) | [**fetch**](#fetch) | [**pull**](#pull) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| [**push**](#push) | [**merge**](#merge) | [**tag**](#tag) |

### gc

- `git gc`

### init

- `git init`

    initialize a repository in an existing directory

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
