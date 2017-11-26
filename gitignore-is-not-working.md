## Question
My `.gitignore` file seems to be ignored by git - could the `.gitignore` file be corrupt? Which file format, locale or culture does git expect?

My `.gitignore`
```
#this is a comment
debug.log
nbproject/
```

Output from `git status`:
```
# On branch master
# Your branch is ahead of 'origin/master' by 1 commit.
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       debug.log
#       nbproject/
nothing added to commit but untracked files present (use "git add" to track)
```

I would like debug.log and nbproject/ not to appear in the untracked files list.

Where should I start looking to fix this?

## Answer
Even if you haven't tracked the files so far, git seems to be able to "know" about them even after you add them to `.gitignore`.

**NOTE : First commit your current changes, or you will lose them.**

Then run the following commands from the top folder of your git repo:
```
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```

## References
1. [.gitignore is not working](https://stackoverflow.com/questions/11451535/gitignore-is-not-working)