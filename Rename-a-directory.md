## Question
In a Git repository, how to properly rename a directory? I think it should work to copy the directory to be renamed to a new directory with desired name, and delete the old directory, and `git add`, `git commit` and `push` everything. But is this the best way?

## Answer
Basic rename (or move):
```
git mv <old name> <new name>
```

Case sensitive rename—eg. from **casesensitive** to **CaseSensitive**—you must use a two step:
```
git mv casesensitive tmp
git mv tmp CaseSensitive
```
([More about case sensitivity in Git…](https://stackoverflow.com/questions/17683458/how-do-i-commit-case-sensitive-only-filename-changes-in-git/17688308#17688308))

…followed by commit and push would be the simplest way to rename a directory in a git repo.

## References

1. [In a Git repository, how to properly rename a directory?](https://stackoverflow.com/questions/11183788/in-a-git-repository-how-to-properly-rename-a-directory)