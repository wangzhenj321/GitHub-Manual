## Description

Given one or more existing commits, revert the changes that the related patches introduce, and record some new commits that record them. **This requires your working tree to be clean (no modifications from the HEAD commit).**

## Synopsis

- `git revert [--[no-]edit] [-n] [-m parent-number] [-s] [-S[<keyid>]] <commit>...`

- `git revert --continue`

- `git revert --quit`

- `git revert --abort`

## Options

- `<commit>...`

    Commits to revert.

- `-e, --edit`

    With this option, `git revert` will let you edit the commit message prior to committing the revert. This is the default if you run the command from a terminal.
    
    - `--no-edit`
    
        With this option, `git revert` will not start the commit message editor.

- `-n, --no-commit`

    Usually the command automatically creates some commits with commit log messages stating which commits were reverted. This flag applies the changes necessary to revert the named commits to your working tree and the index, but does not make the commits. **In addition, when this option is used, your index does not have to match the HEAD commit.** The revert is done against the beginning state of your index.
    
    > **This is useful when reverting more than one commits' effect to your index in a row.**

- `--continue`

    Continue the operation in progress using the information in `.git/sequencer`. Can be used to continue after resolving conflicts in a failed `cherry-pick` or `revert`.

- `--quit`

    Forget about the current operation in progress. Can be used to clear the sequencer state after a failed `cherry-pick` or `revert`.

- `--abort`

    Cancel the operation and return to the pre-sequence state.
