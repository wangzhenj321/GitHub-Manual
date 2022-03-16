## Description

Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository, and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

After the clone, a plain `git fetch` without arguments will update all the remote-tracking branches, and a `git pull` without arguments will in addition merge the remote master branch into the current master branch, if any.

This default configuration is achieved by creating references to the remote branch heads under `refs/remotes/origin` and by initializing `remote.origin.url` and `remote.origin.fetch` configuration variables.

## Synopsis

- `git clone [-o <name>] [-b <name>] <repository>`

## Options

- `-o <name>, --origin <name>`

    Instead of using the remote name `origin` to keep track of the upstream repository, use `<name>`. Overrides `clone.defaultRemoteName` from the config.

- `-b <name>, --branch <name>`

    Instead of pointing the newly created `HEAD` to the branch pointed to by the cloned repository’s `HEAD`, point to `<name>` branch instead. In a non-bare repository, this is the branch that will be checked out. `--branch` can also take tags and detaches the `HEAD` at that commit in the resulting repository.
