## Description

**Use `git stash` when you want to record the current state of the working directory and the index, but want to go back to a clean working directory.** The command saves your local modifications away and reverts the working directory to match the HEAD commit.

The modifications stashed away by this command can be listed with `git stash list`, inspected with `git stash show`, and restored (potentially on top of a different commit) with `git stash apply`. Calling `git stash` without any arguments is equivalent to `git stash save`. A stash is by default listed as "WIP on branchname ...", but you can give a more descriptive message on the command line when you create one.

The latest stash you created is stored in **refs/stash**(`.git/refs/stash`); older stashes are found in the **reflog**(`.git/logs/refs/stash`) of this reference and can be named using the usual reflog syntax (e.g. stash@{0} is the most recently created stash, stash@{1} is the one before it, stash@{2.hours.ago} is also possible).

## Synopsis

- `git stash list [<options>]`
- `git stash show [<stash>]`
- `git stash drop [-q|--quiet] [<stash>]`
- `git stash ( pop | apply ) [--index] [-q|--quiet] [<stash>]`
- `git stash branch <branchname> [<stash>]`
- `git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet] [-u|--include-untracked] [-a|--all] [<message>]]`
- `git stash clear`

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

If the `--index` option is used, then tries to reinstate not only the working tree’s changes, but also the index’s ones. However, this can fail,
when you have conflicts (which are stored in the index, where you therefore can no longer apply the changes as they were originally).

When no <stash> is given, stash@{0} is assumed, otherwise <stash> must be a reference of the form stash@{<revision>}.

### `git stash apply [--index] [-q|--quiet] [<stash>]`

#### `git stash branch <branchname> [<stash>]`
#### `git stash [save [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet] [-u|--include-untracked] [-a|--all] [<message>]]`
#### `git stash clear`
#### `git stash create [<message>]`
#### `git stash store [-m|--message <message>] [-q|--quiet] <commit>`
