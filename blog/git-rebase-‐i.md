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

## Example

**Step 1:** `git log`

![](../img/git-rebase--i/git-log.png?raw=true)

**Step 2:** `git rebase -i HEAD~3`

![](../img/git-rebase--i/git-rebase-i.png?raw=true)

## References
1. [Remove 4 commits from my git history](https://stackoverflow.com/questions/11113322/remove-4-commits-from-my-git-history)
