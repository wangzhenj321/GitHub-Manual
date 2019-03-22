## Description
    
## Synopsis

- `git merge [-n] [--stat] [--no-commit] [--squash] [--[no-]edit] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]] [--[no-]rerere-autoupdate] [-m <msg>] [<commit>...]`

- `git merge --abort`

## Options

- `--commit, --no-commit`

    Perform the **merge** and **commit** the result. This option can be used to override `--no-commit`.

    With `--no-commit` perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.
    
    > Refer to: [Git merge without auto commit](https://stackoverflow.com/questions/8640887/git-merge-without-auto-commit)
    > 
    > **However, with `--no-commit`, when the merge resolves as a fast-forward, it still autocommits. At this special case, the option `--no-ff` is need.**

- `--ff`

    When the merge resolves as a fast-forward, only update the branch pointer, without creating a merge commit. This is the default behavior.
    
    - `--no-ff`
    
        Create a merge commit even when the merge resolves as a fast-forward. This is the default behaviour when merging an annotated (and possibly signed) tag.
    
    - `--ff-only`
    
        Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a fast-forward.

- `--squash, --no-squash`

Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make a commit, move the HEAD, or record $GIT_DIR/MERGE_HEAD (to cause the next git commit command to create a merge commit). This allows you to create a single commit on top of the current branch whose effect is the same as merging another branch
(or more in case of an octopus).

With --no-squash perform the merge and commit the result. This option can be used to override --squash.
