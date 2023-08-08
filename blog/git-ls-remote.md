## Description

Displays references available in a remote repository along with the associated commit IDs.

## Synopsis

- `git ls-remote [--heads] [--tags] [<repository> [<patterns>...]]`

## Options

- `-h, --heads, -t, --tags`

    Limit to only refs/heads and refs/tags, respectively. These options are not mutually exclusive; when given both, references stored in refs/heads and refs/tags are displayed.

- `<repository>`

    The "remote" repository to query. This parameter can be either a URL or the name of a remote.
