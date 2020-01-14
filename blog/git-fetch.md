## Description

Fetch branches and/or tags (collectively, "refs") from one or more other repositories, along with the objects necessary to complete their histories. Remote-tracking branches are updated (see the description of `<refspec>` below for ways to control this behavior).

`git fetch` can fetch from either a single named repository or URL, or from several repositories at once if `<group>` is given and there is a `remotes.<group>` entry in the configuration file.

## Synopsis

- `git fetch [<options>] [<repository> [<refspec>...]]`

## Options

- `<repository>`

    The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT URLS below) or the name of a remote (see the section REMOTES below).

- `<refspec>`

    Specifies which refs to fetch and which local refs to update. When no `<refspec>`s appear on the command line, the refs to fetch are read from `remote.<repository>.fetch` variables instead (see CONFIGURED REMOTE-TRACKING BRANCHES below).
    
    The format of a `<refspec>` parameter is an optional plus +, followed by the source ref `<src>`, followed by a colon :, followed by the destination ref `<dst>`. The colon can be omitted when `<dst>` is empty.
    
    The remote ref that matches `<src>` is fetched, and if `<dst>` is not empty string, the local ref that matches it is fast-forwarded using `<src>`. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

## GIT URLS

In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository. Depending on the transport protocol, some of this information may be absent.

Git supports ssh, git, http, and https protocols (in addition, ftp, and ftps can be used for fetching and rsync can be used for fetching and pushing, but these are inefficient and deprecated; do not use them).

The native transport (i.e. git:// URL) does no authentication and should be used with caution on unsecured networks.

The following syntaxes may be used with them:

- ssh://[user@]host.xz[:port]/path/to/repo.git/
- git://host.xz[:port]/path/to/repo.git/
- http[s]://host.xz[:port]/path/to/repo.git/
- ftp[s]://host.xz[:port]/path/to/repo.git/
- rsync://host.xz/path/to/repo.git/

An alternative scp-like syntax may also be used with the ssh protocol:

- [user@]host.xz:path/to/repo.git/

This syntax is only recognized if there are no slashes before the first colon. This helps differentiate a local path that contains a colon. For example the local path `foo:bar` could be specified as an absolute path or `./foo:bar` to avoid being misinterpreted as an ssh url.

The ssh and git protocols additionally support `~username` expansion:

- ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/
- git://host.xz[:port]/~[user]/path/to/repo.git/
- [user@]host.xz:/~[user]/path/to/repo.git/

For local repositories, also supported by Git natively, the following syntaxes may be used:

- /path/to/repo.git/
- file:///path/to/repo.git/

These two syntaxes are mostly equivalent, except when cloning, when the former implies `--local` option.
