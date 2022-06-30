## Description

Reads the supplied diff output (i.e. "a patch") and applies it to files. When running from a subdirectory in a repository, patched paths outside the directory are ignored. With the `--index` option the patch is also applied to the index, and with the `--cached` option the patch is only applied to the index. Without these options, the command applies the patch only to files, and does not require them to be in a Git repository.

This command applies the patch but does not create a commit.

## Synopsis

`git apply [<patch>...]`

## Options

- `<patch>...`

    The files to read the patch from. `-` can be used to read from the standard input.

- `--stat`

    Instead of applying the patch, output diffstat for the input. Turns off "apply".

- `--check`

    Instead of applying the patch, see if the patch is applicable to the current working tree and/or the index file and detects errors. Turns off "apply".

- `--index`

    Apply the patch to both the index and the working tree (or merely check that it would apply cleanly to both if `--check` is in effect). Note that `--index` expects index entries and working tree copies for relevant paths to be identical (their contents and metadata such as file mode must match), and will raise an error if they are not, even if the patch would apply cleanly to both the index and the working tree in isolation.

- `--cached`

    Apply the patch to just the index, without touching the working tree. If `--check` is in effect, merely check that it would apply cleanly to the index entry.
