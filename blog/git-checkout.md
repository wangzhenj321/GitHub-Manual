## Description

- `git checkout [-q] [-f] [-m] [<branch>]`

    > :heavy_check_mark: **switch**

    To prepare for working on `<branch>`, **switch** to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.

- `git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]`

    > :heavy_check_mark: **create**

    Specifying `-b` causes a new branch to be **created** as if `git branch` were called and then checked out.

- `git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]`

    > :heavy_check_mark: :star: **update**

    When `<paths>` or `--patch` are given, git checkout does not switch branches. It **updates** the named paths in the working tree from the index file or from a named `<tree-ish>` (most often a commit).

## Synopsis

- `git checkout [-q] [-f] [-m] [<branch>]`

- `git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]`

- `git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]`

## Options

- `<start_point>`

    The name of a commit at which to start the new branch. Defaults to HEAD.

- `<tree-ish>`

    Tree to checkout from (when paths are given). If not specified, the index will be used.

## Examples

1. Reset or revert a specific file to a specific revision using Git?

    > Refer to: https://stackoverflow.com/questions/215718/reset-or-revert-a-specific-file-to-a-specific-revision-using-git?rq=1

    **Q:** I have made some changes to a file which has been committed a few times as part of a group of files, but now want to reset/revert the changes on it back to a previous version.
    
    **A:** Assuming the hash of the commit you want is `c5f567`:
    
    ```
    git checkout c5f567 -- file1/to/restore file2/to/restore
    ```
    
    - **Step 1:** `git log -p`
    
        <img src="../img/git-checkout/git_log_p">
    
    - **Step 2:** `git checkout 965870a2030b7b8bac39e5c2467543b1461451a4 -- blog/git-rm.md`
    
        <img src="../img/git-checkout/git_checkout_update">
    
    - **Step 3:** `git log --stat`
    
        <img src="../img/git-checkout/git_log_stat">
