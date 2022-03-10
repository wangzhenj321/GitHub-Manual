## Description

Runs a number of housekeeping tasks within the current repository, such as compressing file revisions (to reduce disk space and increase performance), removing unreachable objects which may have been created from prior invocations of git add, packing refs, pruning reflog, rerere metadata or stale working trees. May also update ancillary indexes such as the commit-graph.

When common porcelain operations that create objects are run, they will check whether the repository has grown substantially since the last maintenance, and if so run `git gc` automatically. See `gc.auto` below for how to disable this behavior.

Running `git gc` manually should only be needed when adding objects to a repository without regularly running such porcelain commands, to do a one-off repository optimization, or e.g. to clean up a suboptimal mass-import.

## Synopsis

- `git gc [--aggressive] [--auto] [--quiet] [--prune=<date> | --no-prune] [--force] [--keep-largest-pack]`

## Options

- `--aggressive`

    Usually `git gc` runs very quickly while providing good disk space utilization and performance. This option will cause `git gc` to more aggressively optimize the repository at the expense of taking much more time. The effects of this optimization are mostly persistent.
