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

---

**`git merge` will also include the currently checked-out branch in the merged version.** So if you have branch1 checked out, and you run `git merge branch2 branch3`, the merged version will combine branch1 as well as branch2 and branch3. That’s because the branch1 label will update after you make the merge commit, so it’s unlikely that you didn’t want the changes from branch1 included in the merge. For this reason, you should always checkout one of the two branches you’re planning on merging before doing the merge. Which one you should check out depends on which branch label you want to point to the new commit.

Since the checked-out branch is always included in the merge, you may have guessed that when you are merging two branches, you don't need to specify both of them as arguments to `git merge` on the command line. If you want to merge branch2 into branch1, you can simply `git checkout branch1` and then type `git merge branch2`. The only reason to type `git merge branch1 branch2` is if it helps you keep better mental track of which branches you are merging. 

Also, since the two branches are merged, the order in which they are typed into the command line does not matter. The key is to remember that `git merge` always merges all the specified branches into the currently checked out branch, creating a new commit for that branch.

---

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

- `<commit>...`

    Commits, usually other branch heads, to merge into our branch.
