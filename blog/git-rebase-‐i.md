## Question
I have done some commits and pushed them into my repository. Then I did a pull request but I realized there are some commits I don't want to be in the pull request.

They look like this:
```
My commits look like this:

Correct HTML    
ab1c41c 

HTML escaping   
8b38955 

Merge branch 'master' into internationalized    
2854662

Modified config 
b942f13 

tried pushing   
b73d792 

Added assets    
f20106e 

Added config    
408118f 

Fixed views conflicts   
86f2509 

added layouts   
da27e11 

Fixed layout markup
92d6bcc 
```
If I want to get rid of these commits:
```
Modified config 
b942f13 

tried pushing   
b73d792 

Added assets    
f20106e 

Added config    
408118f 
```
How do I do it? Notice that I want to keep these ones which are before in time that the ones i want to delete:
```
Correct HTML    
ab1c41c 

HTML escaping   
8b38955
```

## Answer
You can do an [interactive rebase](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History).

Assuming your head is at `ab1c41c` from your example, invoke the rebase as follows
```
git rebase -i HEAD~7
```
**This tells git you want to manipulate the last 8 or so commits. You'll be dropped into your editor with a listing of the commits and some instructions.**

---

**Remarks:** For convenient edit operation, it's better to setup an editor, such as Sublime Text, as Git message editor.

---

Delete the lines that contain the commits to remove, save and quit. Git will preform the rebase, and that's it.

Keep in mind, because of the rebase, if you want to push to the same branch you'll need to pass the option `--force`.

**Disclaimer** Rebasing and force pushing can cause you to lose work or piss people off, so just make sure you understand what you're doing. :)

## Example 1

**Step 1:** `git log`

![](../img/git-rebase--i/git-log.png?raw=true)

**Step 2:** `git rebase -i HEAD~3`

![](../img/git-rebase--i/git-rebase-i.png?raw=true)

## Example 2 dummy merge commits from github website

**Step 1:** `git log --graph`

The `Author: Kazumi Iwane <32505663+kazumi-iwane@users.noreply.github.com>` of the `commit 8161de79823e4ef4550fec5a427682d463737cc3` shows that this commit is a dummy commit due to the merge operation on github. The so-called dummy merge commit means that this commit contains no modification but only merges some commits into the mainline branch. In general, this kind of commit occurs while merging the commits of a pull request into the mainline branch, and it will influence the number of manipulatable commits of the command `git rebase -i`. 

![](../img/git-rebase--i/git-log-dummy-merge.png?raw=true)

**Step 2:** `git rebase -i HEAD~2`

The `HEAD~2` means that the newest two commits are the manipulatable commits. From the view of commit list, these two commits are

```
commit 8161de79823e4ef4550fec5a427682d463737cc3
commit 6a79e4db7ba0e82c8a0a52d0e1b95da1f6c02dfd
```

instead of

```
commit 8161de79823e4ef4550fec5a427682d463737cc3
commit 4aa46738723b6ae1ca366cf064c3e27b0c6e99ee
```

---

**Remarks:** Please use `git log --graph` instead of `git log` to show the commit list.

---

Since the `commit 8161de79823e4ef4550fec5a427682d463737cc3` is the dummy merge commit, so all merged commits in this dummy merge commit (***no matter how many of them***) become the manipulatable commits. In this example, only `commit 4aa46738723b6ae1ca366cf064c3e27b0c6e99ee` becomes the manipulatable commit. Finally, the two manipulatable commits shown as the following figure are 

```
commit 4aa46738723b6ae1ca366cf064c3e27b0c6e99ee
commit 6a79e4db7ba0e82c8a0a52d0e1b95da1f6c02dfd
```

![](../img/git-rebase--i/git-rebase-i-dummy-merge.png?raw=true)

If the manipulatable commit is the dummy merge commit, all merged commits of it replace it to become the manipulatable commits. This also means that this dummy merge commits will be removed from the commit history, even though there is no operation in `git rebase -i`. 

## References
1. [Remove 4 commits from my git history](https://stackoverflow.com/questions/11113322/remove-4-commits-from-my-git-history)
