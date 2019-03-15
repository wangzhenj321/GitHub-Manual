## Description

> The `<tree-ish>/<commit>` defaults to HEAD in all forms.

- `git reset [-q] [<tree-ish>] [--] <paths>...`

    This form resets the index entries for all `<paths>` to their state at `<tree-ish>`. (It does not affect the working tree or the current branch.)

- `git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]`

    This form resets the current branch **head to** `<commit>` and possibly updates the index (resetting it to the tree of <commit>) and the working tree depending on `<mode>`. If `<mode>` is omitted, defaults to `--mixed`. The `<mode>` must be one of the following:

    - `--soft`
    
        Does not touch the index file or the working tree at all (but resets the head to `<commit>`, just like all modes do). This leaves all your changed files "Changes to be committed", as `git status` would put it.
    
    - `--mixed`
    
        Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.
    
    - `--hard`
    
        Resets the index and working tree. Any changes to tracked files in the working tree since `<commit>` are discarded.
    
    - `--merge`
    
    - `--keep`

## Synopsis

- `git reset [-q] [<tree-ish>] [--] <paths>...`

- `git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]`

## Examples

1. `git reset --hard HEAD~3`

    The last three commits (**HEAD**, **HEAD^**, and **HEAD~2**) were bad and you do not want to ever see them again.

2. `git reset --hard`

    This is a synonym for `git reset --hard HEAD` clears the mess from the index file and the working tree.
