## Description

> In most cases, users should run `git gc`, which calls `git prune`.

This runs `git fsck --unreachable` using all the refs available in `refs/`, optionally with additional set of objects specified on the command line, and prunes all unpacked objects unreachable from any of these head objects from the object database. In addition, it prunes the unpacked objects that are also found in packs by running `git prune-packed`. It also removes entries from `.git/shallow` that are not reachable by any ref.

Note that unreachable, packed objects will remain. If this is not desired, see `git repack`.

## Synopsis

- `git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…]`

## Options
