https://git-scm.com/docs/git-submodule

https://git-scm.com/docs/gitmodules

https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration


## `add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--depth <depth>] [--] <repository> [<path>]`

Add the given repository as a submodule at the given path to the changeset to be committed next to the current project: the current project is termed the "superproject".

\<repository\> is the URL of the new submodule’s origin repository. This may be either an absolute URL, or (if it begins with ./ or ../), the location relative to the superproject’s default remote repository.
  
The optional argument <path> is the relative location for the cloned submodule to exist in the superproject. If <path> is not given, the canonical part of the source repository is used ("repo" for "/path/to/repo.git" and "foo" for "host.xz:foo/.git").


## `status [--cached] [--recursive] [--] [<path>…]`

Show the status of the submodules. This will print the SHA-1 of the currently checked out commit for each submodule, along with the submodule path and the output of git describe for the SHA-1.


## `update [--init] [--remote] [-N|--no-fetch] [--[no-]recommend-shallow] [-f|--force] [--checkout|--rebase|--merge] [--reference <repository>] [--depth <depth>] [--recursive] [--jobs <n>] [--] [<path>…]`

The *update* procedures supported both from the command line as well as through the `submodule.<name>.update` configuration are:

- **checkout** (default)
- **rebase**
- **merge**
- **custom command**
- **none**



## `foreach [--recursive] <command>`

