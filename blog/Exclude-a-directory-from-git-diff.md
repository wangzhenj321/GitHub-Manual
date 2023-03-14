## Question

I'm wondering how I can exclude an entire directory from my Git diff. (In this case /spec). I'm creating a diff for our entire software release using the git diff command. However the changes to the specs are irrelevant for this procedure, and just create headaches. now I know i can do

```
git diff previous_release..current_release app/
```

This would create a diff for all the changes in the app directory, but not for instance, in the lib/ directory. Does anyone know how to accomplish this task? Thanks!

Edit: I just want to be clear, I know I can just string the parameters of all of my directories on the end, minus /spec. I was hoping there was a way to truly exclude a single directory in the command.

## Answer

You can also use:

```
git diff previous_release..current_release -- . ':!spec'
```

This is a newish git feature which allows excluding certain paths. It should be more reliable than various shell oneliners.

Since Git 2.13 (Q2 2017), you can replace ! with ^. The latter doesn't need quotes. So you can write it as:

```
git diff previous_release..current_release -- . :^spec
```

## Reference

1. [Exclude a directory from git diff](https://stackoverflow.com/questions/4380945/exclude-a-directory-from-git-diff)
