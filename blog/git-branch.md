## Description

- `git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]`

    This command creates a new branch head named `<branchname>` which points to the current **HEAD**, or `<start-point>` if given.

- `git branch (-m | -M) [<oldbranch>] <newbranch>`

   With a -m or -M option, <oldbranch> will be renamed to <newbranch>. If <oldbranch> had a corresponding reflog, it is renamed to match <newbranch>, and a reflog entry is created to remember
the branch renaming. If <newbranch> exists, -M must be used to force the rename to happen.

- `git branch (-d | -D) [-r] <branchname>...`

## Synopsis

- `git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]`

- `git branch (-m | -M) [<oldbranch>] <newbranch>`

- `git branch (-d | -D) [-r] <branchname>...`

## Options
