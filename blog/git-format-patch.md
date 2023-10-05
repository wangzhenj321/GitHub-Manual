## Description

Prepare patches for e-mail submission.

## Synopsis

`git format-patch [ <since> | <revision range> ]`

## Options

- `-<n>`

    Prepare patches from the topmost <n> commits.

## Examples

1. Extract three topmost commits from the current branch and format them as e-mailable patches:

    ```
    $ git format-patch -3
    ```
