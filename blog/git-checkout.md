## Description

- `git checkout [-q] [-f] [-m] [<branch>]`

    > :heavy_check_mark: **switch**

    To prepare for working on `<branch>`, **switch** to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.

- `git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]`

    > :heavy_check_mark: **create**

    Specifying `-b` causes a new branch to be **created** as if `git branch` were called and then checked out.

- `git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]`

    > :heavy_check_mark: **update**

    When `<paths>` or `--patch` are given, git checkout does not switch branches. It **updates** the named paths in the working tree from the index file or from a named `<tree-ish>` (most often a commit).

## Synopsis

- `git checkout [-q] [-f] [-m] [<branch>]`

- `git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]`

- `git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]`

## Options
