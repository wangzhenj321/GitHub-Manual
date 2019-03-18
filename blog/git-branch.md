## Description

- `git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]`

    This command **creates** a new branch head named `<branchname>` which points to the current HEAD, or `<start-point>` if given.

- `git branch (-m | -M) [<oldbranch>] <newbranch>`

   With a `-m` or `-M` option, `<oldbranch>` will be **renamed** to `<newbranch>`. If `<oldbranch>` had a corresponding reflog, it is renamed to match `<newbranch>`, and a reflog entry is created to remember the branch renaming. If `<newbranch>` exists, `-M` must be used to force the rename to happen.

- `git branch (-d | -D) [-r] <branchname>...`

    With a `-d` or `-D` option, `<branchname>` will be **deleted**. If the branch currently has a reflog then the reflog will also be deleted. Use `-r` together with `-d` to delete remote-tracking branches.
    
    > **Note, that it only makes sense to delete remote-tracking branches if they no longer exist in the remote repository or if `git fetch` was configured not to fetch them again.**

## Synopsis

- `git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]`

- `git branch (-m | -M) [<oldbranch>] <newbranch>`

- `git branch (-d | -D) [-r] <branchname>...`

## Options

- `-d, --delete`

    Delete a branch. The branch must be fully merged in its upstream branch, or in HEAD if no upstream was set with `--track` or `--set-upstream`.
    
    - `-D`
    
        Shortcut for `--delete --force`.

- `-f, --force`

- `-m, --move`

    Move/rename a branch and the corresponding reflog.
    
    - `-M`
    
        Shortcut for `--move --force`.

- `-r, --remotes`

    List or delete (if used with `-d`) the remote-tracking branches.

- `-a, --all`

    List both remote-tracking branches and local branches.
