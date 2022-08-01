## Description

Splits mail messages in a mailbox into commit log message, authorship information and patches, and applies them to the current branch.

## Synopsis

- `git am [(<mbox> | <Maildir>)...]`

## Options

- `(<mbox>|<Maildir>)...`

    The list of mailbox files to read patches from. If you do not supply this argument, the command reads from the standard input. If you supply directories, they will be treated as Maildirs.
