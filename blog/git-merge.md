## Description

- `git merge [--no-commit] [--ff] [--squash] [-m <msg>] [<commit>...]`

    Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch.

    **From:**
    ```
         A---B---C topic
        /
    D---E---F---G master
    ```
    
    **To:**
    ```
         A---B---C topic
        /         \
    D---E---F---G---H master
    ```

- `git merge --abort`

    This syntax can only be run after the merge has resulted in conflicts. `git merge --abort` will abort the merge process and try to reconstruct the pre-merge state.
    
    However, if there were **uncommitted changes** when the merge started (and especially if those changes were further modified after the merge was started), `git merge --abort` will in some cases be **unable** to reconstruct the original (pre-merge) changes.
    
    > **Warning:** Running `git merge` with non-trivial uncommitted changes is discouraged: while possible, it may leave you in a state that is hard to back out of in the case of a conflict.

## Synopsis

- `git merge [--no-commit] [--ff] [--squash] [-m <msg>] [<commit>...]`

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

    > Refer to [`git merge --squash`](git-merge-rebase-squash.md#git-merge---squash)

- `-m <msg>`

    Set the commit message to be used for the merge commit (in case one is created).
