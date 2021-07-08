## Description

Stores the current contents of the index in a new commit along with a log message from the user describing the changes.

## Synopsis

`git commit [--amend] [-F <file> | -m <msg>]`

## Options

- `--amend`

    Replace the tip of the current branch by creating a new commit. The recorded tree is prepared as usual (including the effect of the `-i` and `-o` options and explicit pathspec), and the message from the original commit is used as the starting point, instead of an empty message, when no other message is specified from the command line via options such as `-m`, `-F`, `-c`, etc. The new commit has the same parents and author as the current one (the `--reset-author` option can countermand this).

- `-m <msg>, --message=<msg>`

    Use the given <msg> as the commit message. If multiple `-m` options are given, their values are concatenated as separate paragraphs. The `-m` option is mutually exclusive with `-c`, `-C`, and `-F`.

## Examples

1. Amend the most recent commit message.
    
    ```
    git commit --amend -m "New commit message"
    ```
    
