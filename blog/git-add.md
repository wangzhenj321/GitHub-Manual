## Description

This command updates the index using the current content found in the working tree, to prepare the content staged for the next commit. It typically adds the current content of existing paths as a whole, but with some options it can also be used to add content with only part of the changes made to the working tree files applied, or remove paths that do not exist in the working tree anymore.

> **The `git add` command will not add ignored files by default.** If any ignored files were explicitly specified on the command line, `git add` will fail with a list of ignored files. Ignored files reached by **directory recursion** or **filename globbing** performed by Git (quote your globs before the shell) will be silently ignored. The `git add` command can be used to add ignored files with the `-f` (force) option.

## Synopsis

```
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
         [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
         [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing]
         [--] [<pathspec>...]
```

## Options

- `<pathspec>...`

    Files to add content from.
    
    > **Fileglobs** (e.g. `*.c`) can be given to add all matching files.
    
    > Also a **leading directory** name (e.g. dir to add `dir/file1` and `dir/file2`) can be given to update the index to match the current state of the directory as a whole.

- `-f, --force`

    Allow adding otherwise ignored files.

- `-u, --update`

    Update the index just where it already has an entry matching `<pathspec>`. This removes as well as modifies index entries to match the working tree, **but adds no new files**.
    
    If no `<pathspec>` is given when `-u` option is used, all tracked files in the entire working tree are updated (old versions of Git used to limit the update to the current directory and its subdirectories).

- `-A, --all, --no-ignore-removal`

    Update the index not only where the working tree has a file matching `<pathspec>` but also where the index already has an entry. **This adds, modifies, and removes index entries to match the working tree.**
    
    If no `<pathspec>` is given when `-A` option is used, all files in the entire working tree are updated (old versions of Git used to limit the update to the current directory and its subdirectories).

- `--`

    This option can be used to separate command-line options from the list of files (useful when filenames might be mistaken for command-line options).
