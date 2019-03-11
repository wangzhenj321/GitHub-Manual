## Description

Manage the set of repositories ("remotes") whose branches you track.

## Synopsis

- `git remote [-v | --verbose]`

- `git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=<fetch|push>] <name> <url>`

- `git remote rename <old> <new>`

- `git remote remove <name>`

- `git remote set-url [--push] <name> <newurl> [<oldurl>]`

- `git remote [-v | --verbose] show [-n] <name>...`

- `git remote prune [-n | --dry-run] <name>...`

## Options

- `-v, --verbose`

    Be a little more verbose and show remote url after name. NOTE: This must be placed between remote and subcommand.

## Commands

- `add`

    Adds a remote named `<name>` for the repository at `<url>`. The command `git fetch <name>` can then be used to create and update remote-tracking branches `<name>/<branch>`.

- `rename`

    Rename the remote named `<old>` to `<new>`. All remote-tracking branches and configuration settings for the remote are updated.

- `remove`

    Remove the remote named `<name>`. All remote-tracking branches and configuration settings for the remote are removed.

- `set-url`

    Changes URLs for the remote. Sets first URL for remote `<name>` that matches regex `<oldurl>` (first URL if no `<oldurl>` is given) to `<newurl>`. If `<oldurl>` doesn’t match any URL, an error occurs and nothing is changed.

- `show`

    Gives some information about the remote `<name>`.

- `prune`

    Deletes all stale remote-tracking branches under `<name>`. These stale branches have already been removed from the remote repository referenced by `<name>`, but are still locally available in "remotes/<name>".

    With `--dry-run` option, report what branches will be pruned, but do not actually prune them.
