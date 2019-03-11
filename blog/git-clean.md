**Table of Contents**

[Part 1: What's untracked files?](#part-1-whats-untracked-files)

[Part 2: How to remove untracked files?](#part-2-how-to-remove-untracked-files)


# Part 1: What's untracked files?

Remember that each file in your working directory can be in one of two states: **tracked** or **untracked**. 

- **Tracked files** are files that were in the last snapshot; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.

- **Untracked files** are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area. When you first clone a repository, all of your files will be tracked and unmodified because Git just checked them out and you haven’t edited anything.

As you edit files, Git sees them as modified, because you’ve changed them since your last commit. As you work, you selectively stage these modified files and then commit all those staged changes, and the cycle repeats.

![](../img/git-clean/untracked_file.png?raw=true)

## References

1. [Git Basics - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

# Part 2: How to remove untracked files?

## Question
How do you delete untracked local files from your current working tree?

## Answer
As per the Git Documentation `git clean`
> Remove untracked files from the working tree

Step 1 is to show what will be deleted by using the `-n` option:

```
git clean -n
```

Clean Step - **beware: this will delete files**:

```
git clean -f
```

- To remove directories, run `git clean -f -d` or `git clean -fd`
- To remove ignored files, run `git clean -f -X` or `git clean -fX`
- To remove ignored and non-ignored files, run `git clean -f -x` or `git clean -fx`
**Note** the case difference on the X for the two latter commands.

If `clean.requireForce` is set to "true" (the default) in your configuration, one needs to specify `-f` otherwise nothing will actually happen.

### Options

- `-d`

Remove untracked directories in addition to untracked files.

> **If an untracked directory is managed by a different Git repository, it is not removed by default. Use `-f` option twice if you really want to remove such a directory.**

- `-f, --force`

If the Git configuration variable `clean.requireForce` is not set to false, `git clean` will refuse to run unless given `-f`, `-n` or `-i`.

> **Git will refuse to delete directories with `.git` sub directory or file unless a second `-f` is given.**

- `-n, --dry-run`

Don’t actually remove anything, just show what would be done.

- `-x`

Don’t use the standard ignore rules read from .gitignore (per directory) and $GIT_DIR/info/exclude, but do still use the ignore rules given with -e options. **This allows removing all untracked files, including build products.** This can be used (possibly in conjunction with `git reset`) to create a pristine working directory to test a clean build.

- `-X`

Remove **only** files ignored by Git. This may be useful to rebuild everything from scratch, but keep manually created files.

## References

1. [How to remove local (untracked) files from the current Git working tree?](https://stackoverflow.com/questions/61212/how-to-remove-local-untracked-files-from-the-current-git-working-tree)
