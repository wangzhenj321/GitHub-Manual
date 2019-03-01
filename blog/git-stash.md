## Description

**Use `git stash` when you want to record the current state of the working directory and the index, but want to go back to a clean working directory.** The command saves your local modifications away and reverts the working directory to match the HEAD commit.

The modifications stashed away by this command can be listed with `git stash list`, inspected with `git stash show`, and restored (potentially on top of a different commit) with `git stash apply`. Calling `git stash` without any arguments is equivalent to `git stash save`. A stash is by default listed as "WIP on branchname ...", but you can give a more descriptive message on the command line when you create one.

The latest stash you created is stored in **refs/stash**(`.git/refs/stash`); older stashes are found in the **reflog**(`.git/logs/refs/stash`) of this reference and can be named using the usual reflog syntax (e.g. stash@{0} is the most recently created stash, stash@{1} is the one before it, stash@{2.hours.ago} is also possible).

## Synopsis

- [`git stash list [<options>]`](#git-stash-list-options)

- [`git stash show [<stash>]`](#git-stash-show-stash)

- [`git stash drop [-q|--quiet] [<stash>]`](#git-stash-drop--q--quiet-stash)

- [`git stash pop [--index] [-q|--quiet] [<stash>]`](#git-stash-pop---index--q--quiet-stash)

- [`git stash apply [--index] [-q|--quiet] [<stash>]`](#git-stash-apply---index--q--quiet-stash)

- [`git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet] [-u|--include-untracked] [-a|--all] [<message>]]`](#git-stash-save--p--patch--k--no-keep-index--q--quiet--u--include-untracked--a--all-message)

- [`git stash clear`](#git-stash-clear)

## Options

### `git stash list [<options>]`

List the stashes that you currently have. Each stash is listed with its name (e.g. stash@{0} is the latest stash, stash@{1} is the one before, etc.), the name of the branch that was current when the stash was made, and a short description of the commit the stash was based on.

```
stash@{0}: WIP on submit: 6ebd0e2... Update git-stash documentation
stash@{1}: On master: 9cc0589... Add git-stash
```

The command takes options applicable to the `git log` command to control what is shown and how.

### `git stash show [<stash>]`

Show the changes recorded in the stash as a diff between the stashed state and its original parent. When no `<stash>` is given, shows the latest one. By default, the command shows the diffstat, but it will accept any format known to `git diff` (e.g., `git stash show -p stash@{1}` to view the second most recent stash in patch form). You can use `stash.showStat` and/or `stash.showPatch` config variables to change the default behavior.

### `git stash drop [-q|--quiet] [<stash>]`

Remove a single stashed state from the stash list. When no `<stash>` is given, it removes the latest one. i.e. `stash@{0}`, otherwise `<stash>` must be a valid stash log reference of the form `stash@{<revision>}`.

### `git stash pop [--index] [-q|--quiet] [<stash>]`

Remove a single stashed state from the stash list and apply it on top of the current working tree state, i.e., do the inverse operation of `git stash save`. The working directory must match the index.

**Applying the state can fail with conflicts; in this case, it is not removed from the stash list. You need to resolve the conflicts by hand and call `git stash drop` manually afterwards.**

When no <stash> is given, stash@{0} is assumed, otherwise <stash> must be a reference of the form stash@{<revision>}.

#### `--index`

> If the `--index` option is used, then tries to reinstate not only the working tree’s changes, but also the index’s ones. However, this can fail, when you have conflicts (which are stored in the index, where you therefore can no longer apply the changes as they were originally).

1. Create a stash including both working tree's changes and index's ones.

    ![](../img/git-stash/stash_save_include_index.png?raw=true)

2. Pop the stash without `--index` option.

    ![](../img/git-stash/stash_pop_without_index.png?raw=true)

3. Pop the stash with `--index` option.

    ![](../img/git-stash/stash_pop_with_index.png?raw=true)

### `git stash apply [--index] [-q|--quiet] [<stash>]`

Like `pop`, but do not remove the state from the stash list. Unlike `pop`, `<stash>` may be any commit that looks like a commit created by `stash save` or `stash create`.

### `git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet] [-u|--include-untracked] [-a|--all] [<message>]]`

Save your local modifications to a new stash, and run `git reset --hard` to revert them. The `<message>` part is optional and gives the description along with the stashed state. For quickly making a snapshot, you can omit both "save" and `<message>`, but giving only `<message>` does not trigger this action to prevent a misspelled subcommand from making an unwanted stash.

#### `--keep-index`

> :x: If the `--keep-index` option is used, all changes already added to the index are left intact.

> Refer to [Is "git stash save --keep-index" explained correctly in Chapter 7?](https://github.com/progit/progit2/issues/822)
>
> :heavy_check_mark: `--keep-index` has no effect on what gets captured in the stash, it simply leaves staged content in the index (and, of course, the working tree).

![](../img/git-stash/stash_save_with_keep_index.png?raw=true)

### `git stash clear`

Remove all the stashed states. Note that those states will then be subject to pruning, and may be impossible to recover (see Examples below for a possible strategy).
