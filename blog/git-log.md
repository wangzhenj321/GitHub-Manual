## Description

Shows the commit logs.

## Synopsis

`git log [<options>] [<revision range>] [[--] <path>...]`

## Options

- `--no-decorate, --decorate[=short|full|no]`

    Print out the ref names of any commits that are shown. If short is specified, the ref name prefixes `refs/heads/`, `refs/tags/` and `refs/remotes/` will not be printed. If full is specified, the full ref name (including prefix) will be printed. The default option is short.
        
    <img src="../img/git-log/git_log_decorate.png" width="100%">

- `-<number>, -n <number>, --max-count=<number>`

    Limit the number of commits to output.

- `--pretty[=<format>], --format=<format>`

    Pretty-print the contents of the commit logs in a given format, where `<format>` can be one of `oneline`, `short`, `medium`, `full`, `fuller`, `email`, `raw`, `format:<string>` and `tformat:<string>`.
    
    When `=<format>` part is omitted, it defaults to `medium`.
    
    > **Note: you can specify the default pretty format in the repository configuration.**

- `--abbrev-commit`

    Instead of showing the full 40-byte hexadecimal commit object name, show only a partial prefix. Non default number of digits can be specified with `--abbrev=<n>` (which also modifies diff output, if it is displayed).

- `--oneline`

    This is a shorthand for `--pretty=oneline --abbrev-commit` used together.

- `--graph`

    Draw a text-based graphical representation of the commit history on the left hand side of the output.
        
    <img src="../img/git-log/git_log_graph.png" width="50%">

- `--stat[=<width>[,<name-width>[,<count>]]]`

    Generate a diffstat. By default, as much space as necessary will be used for the filename part, and the rest for the graph part.
    
    <img src="../img/git-log/git_log_stat.png" width="50%">

- `--name-only`

    Show only names of changed files.
    
    <img src="../img/git-log/git_log_name-only.png" width="50%">
