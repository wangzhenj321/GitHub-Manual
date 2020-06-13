https://git-scm.com/book/en/v2/Git-Tools-Submodules

## Part 1 `git submodule`

### `add <repository> [<path>]`

Add the given repository as a submodule at the given path to the changeset to be committed next to the current project: the current project is termed the "superproject".

\<repository\> is the URL of the new submodule’s origin repository. This may be either an absolute URL, or (if it begins with ./ or ../), the location relative to the superproject’s default remote repository.
  
The optional argument <path> is the relative location for the cloned submodule to exist in the superproject. If <path> is not given, the canonical part of the source repository is used ("repo" for "/path/to/repo.git" and "foo" for "host.xz:foo/.git").

The given URL is recorded into `.gitmodules` for use by subsequent users cloning the superproject.

### `status [--recursive] [<path>…]`

Show the status of the submodules. This will print the SHA-1 of the currently checked out commit for each submodule, along with the submodule path and the output of *git describe* for the SHA-1.

If `--recursive` is specified, this command will recurse into nested submodules, and show their status as well.

### `update [--remote] [--checkout|--rebase|--merge] [--recursive]`

The *update* procedures supported both from the command line as well as through the `submodule.<name>.update` configuration are:

- **checkout** (default)
- **rebase**
- **merge**
- **custom command**
- **none**

### `foreach [--recursive] <command>`

### Options

#### `--remote`

This option is only valid for the update command. Instead of using the superproject’s recorded SHA-1 to update the submodule, use the status of the submodule’s remote-tracking branch. The remote used is branch’s remote (`branch.<name>.remote`), defaulting to `origin`. The remote branch used defaults to `master`, but the branch name may be overridden by setting the `submodule.<name>.branch` option in either `.gitmodules` or `.git/config` (with `.git/config` taking precedence).

This works for any of the supported update procedures (`--checkout`, `--rebase`, etc.). The only change is the source of the target SHA-1. For example, `submodule update --remote --merge` will merge upstream submodule changes into the submodules, while `submodule update --merge` will merge superproject gitlink changes into the submodules.

In order to ensure a current tracking branch state, `update --remote` fetches the submodule’s remote repository before calculating the SHA-1. If you don’t want to fetch, you should use `submodule update --remote --no-fetch`.

Use this option to integrate changes from the upstream subproject with your submodule’s current HEAD. Alternatively, you can run `git pull` from the submodule, which is equivalent except for the remote branch name: `update --remote` uses the default upstream repository and `submodule.<name>.branch`, while `git pull` uses the submodule’s `branch.<name>.merge`. Prefer `submodule.<name>.branch` if you want to distribute the default upstream branch with the superproject and `branch.<name>.merge` if you want a more native feel while working in the submodule itself.

> `refs/heads/master` VS `refs/remotes/origin/master`
> 
> The key difference to understand is that the branches under `refs/heads/` are branches that, when you have one checked out, you can advance by creating new commits. Those under `refs/remotes/`, however, are so-called "remote-tracking branches" - these refs just point to the commit that a remote repository was at the last time you did a `git fetch <name-of-remote>`, or a successful `git push` to the corresponding branch in that remote repository.

#### `--merge`

This option is only valid for the update command. Merge the commit recorded in the superproject into the current branch of the submodule. If this option is given, the submodule’s HEAD will not be detached. If a merge failure prevents this process, you will have to resolve the resulting conflicts within the submodule with the usual conflict resolution tools. If the key `submodule.$name.update` is set to `merge`, this option is implicit.

### References

1. [git-submodule](https://git-scm.com/docs/git-submodule)


## Part 2 `.gitmodules`

The `.gitmodules` file, located in the top-level directory of a Git working tree, is a text file with a syntax matching the requirements of `git config`.

The file contains one subsection per submodule, and the subsection value is the name of the submodule. The name is set to the path where the submodule has been added unless it was customized with the `--name` option of *git submodule add*. Each submodule section also contains the following required keys:

**submodule.\<name\>.path**

Defines the path, relative to the top-level directory of the Git working tree, where the submodule is expected to be checked out. The path name must not end with a `/`. All submodule paths must be unique within the .gitmodules file.

**submodule.\<name\>.url**

Defines a URL from which the submodule repository can be cloned. This may be either an absolute URL ready to be passed to `git clone` or (if it begins with ./ or ../) a location relative to the superproject’s origin repository.

In addition, there are a number of optional keys:

**submodule.\<name\>.branch**

A remote branch name for tracking updates in the upstream submodule. If the option is not specified, it defaults to master. A special value of `.` is used to indicate that the name of the branch in the submodule should be the same name as the current branch in the current repository.

### References

1. [gitmodules](https://git-scm.com/docs/gitmodules)
