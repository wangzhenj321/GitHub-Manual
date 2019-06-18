## Description

Show changes between the working tree and the index or a tree, changes between the index and a tree, changes between two trees, changes between two blob objects, or changes between two files on disk.

- `git diff [options] [--] [<path>...]`

    > **index :vs: working tree**

    This form is to view the changes you made **relative to the index** (staging area for the next commit). In other words, the differences are what you could tell Git to further add to the index but you still haven’t.

- `git diff [options] --cached [<commit>] [--] [<path>...]`

    > **tree :vs: index**

    This form is to view the changes you staged for the next commit **relative to the named `<commit>`**. Typically you would want comparison with the latest commit, so if you do not give `<commit>`, it defaults to HEAD. If HEAD does not exist (e.g. unborn branches) and `<commit>` is not given, it shows all staged changes. **`--staged` is a synonym of `--cached`.**

- `git diff [options] <commit> [--] [<path>...]`

    > **tree :vs: working tree**

    This form is to view the changes you have in your working tree **relative to the named `<commit>`**. You can use HEAD to compare it with the latest commit, or a branch name to compare with the tip of a different branch.

- `git diff [options] <commit> <commit> [--] [<path>...]`

    > **tree :vs: tree**

    This is to view the changes between two arbitrary `<commit>`.

- `git diff [options] <blob> <blob>`

    > **blob :vs: blob**

    This form is to view the differences between the raw contents of two blob objects.

## Synopsis

- `git diff [options] [--] [<path>...]`

- `git diff [options] --cached [<commit>] [--] [<path>...]`

- `git diff [options] <commit> [--] [<path>...]`

- `git diff [options] <commit> <commit> [--] [<path>...]`

- `git diff [options] <blob> <blob>`

## Options

- `-p, -u, --patch`

    Generate patch (see section on generating patches). This is the default.

- `--stat[=<width>[,<name-width>[,<count>]]]`

    Generate a diffstat.

- `--name-only`

    Show only names of changed files.

- `<path>...`

    The `<paths>` parameters, when given, are used to limit the diff to the named paths (you can give directory names and get diff for all files under them).
