## Description

You can query/set/replace/unset options with this command.

When **reading**, the values are read from the system, global and repository local configuration files by default, and options `--system`, `--global`, `--local` and `--file <filename>` can be used to tell the command to read from only that location.

When **writing**, the new value is written to the repository local configuration file by default, and options `--system`, `--global`, `--file <filename>` can be used to tell the command to write to that location (you can say `--local` but that is the default).

This command will fail with non-zero status upon error

## Synopsis

- `git config [<file-option>] [type] [-z|--null] name [value [value_regex]]`

- `git config [<file-option>] [type] [-z|--null] --get | --get-all name [value_regex]`

- `git config [<file-option>] --unset | --unset-all name [value_regex]`

- `git config [<file-option>] [-z|--null] [--name-only] -l | --list`

- `git config [<file-option>] -e | --edit`

## Options

- `--get`

    Get the value for a given key (optionally filtered by a regex matching the value). Returns error code 1 if the key was not found and the last value if multiple key values were found.

- `--get-all`

    Like get, but does not fail if the number of values for the key is not exactly one.

- `<file-option>`

    - `--system`
    
        - For **writing** options: write to system-wide `$(prefix)/etc/gitconfig` rather than the repository `.git/config`.
        
        - For **reading** options: read only from system-wide `$(prefix)/etc/gitconfig` rather than from all available files.
    
    - `--global`
    
        - For **writing** options: write to global `~/.gitconfig` file rather than the repository `.git/config`, write to `$XDG_CONFIG_HOME/git/config` file if this file exists and the `~/.gitconfig` file doesn’t.

        - For **reading** options: read only from global `~/.gitconfig` and from `$XDG_CONFIG_HOME/git/config` rather than from all available files.
    
    - `--local`
    
        - For **writing** options: write to the repository `.git/config` file. This is the default behavior.

        - For **reading** options: read only from the repository `.git/config` rather than from all available files.
    
    - `--file config-file`
    
        Use the given config file instead of the one specified by `GIT_CONFIG`.
    
    - `--blob blob`
    
        Similar to `--file` but use the given blob instead of a file.

- `--unset`

    Remove the line matching the key from config file.

- `--unset-all`

    Remove all lines matching the key from config file.

- `-l, --list`

    List all variables set in config file, along with their values.

- `-e, --edit`

    Opens an editor to modify the specified config file; either `--system`, `--global`, or repository (default).

## Files

If not set explicitly with `--file`, there are four files where `git config` will search for configuration options:

> **On Windows (git version 2.16.2.windows.1)**
> 
> ![](../img/git-config/git_config_list_show_origin.png?raw=true)

1. `$(prefix)/etc/gitconfig` :left_right_arrow: `--system`

    System-wide configuration file.

2. `$XDG_CONFIG_HOME/git/config` :left_right_arrow: `--global`

    Second user-specific configuration file. If `$XDG_CONFIG_HOME` is not set or empty, `$HOME/.config/git/config` will be used. Any single-valued variable set in this file will be overwritten by whatever is in `~/.gitconfig`. **It is a good idea not to create this file if you sometimes use older versions of Git, as support for this file was added fairly recently.**

3. `~/.gitconfig` :left_right_arrow: `--global`

    User-specific configuration file. Also called "global" configuration file.

4. `$GIT_DIR/config` :left_right_arrow: `--local`

    Repository specific configuration file.

> The files are read in the order given above, with last value found taking precedence over values read earlier. When multiple values are taken then all values of a key from all files will be used.
> 
> All writing options will per default write to the repository specific configuration file. Note that this also affects options like `--replace-all` and `--unset`. `git config` will only ever change one file at a time.
> 
> You can override these rules either by command-line options or by environment variables. The `--global` and the `--system` options will limit the file used to the global or system-wide file respectively. The `GIT_CONFIG` environment variable has a similar effect, but you can specify any filename you want.

## Environment

- `GIT_CONFIG`

    Take the configuration from the given file instead of `.git/config`. Using the `--global` option forces this to `~/.gitconfig`. Using the `--system` option forces this to `$(prefix)/etc/gitconfig`.

## Configuration File

The Git configuration file contains a number of variables that affect the Git commands' behavior.

- The `.git/config` file in each repository is used to store the configuration for that repository.

- The `$HOME/.gitconfig` is used to store a per-user configuration as fallback values for the `.git/config` file.

- The file `/etc/gitconfig` can be used to store a system-wide default configuration.

The configuration variables are used by both the Git plumbing and the porcelains. The variables are divided into **sections**, wherein the fully qualified variable name of the variable itself is the last dot-separated segment and the section name is everything before the last dot. The variable names are case-insensitive, allow only alphanumeric characters and `-`, and must start with an alphabetic character. Some variables may appear multiple times; we say then that the variable is multivalued.

### Example

```
# Core variables
[core]
       ; Don't trust file modes
       filemode = false

# Our diff algorithm
[diff]
       external = /usr/local/bin/diff-wrapper
       renames = true

[branch "devel"]
       remote = origin
       merge = refs/heads/devel
```

### Popular variables

- `user.name`

    Your full name to be recorded in any newly created commits. Can be overridden by the `GIT_AUTHOR_NAME` and `GIT_COMMITTER_NAME` environment variables.

- `user.email`

    Your email address to be recorded in any newly created commits. Can be overridden by the `GIT_AUTHOR_EMAIL`, `GIT_COMMITTER_EMAIL`, and `EMAIL` environment variables.

- `core.editor`

    Commands such as `commit` and `tag` that lets you edit messages by launching an editor uses the value of this variable when it is set, and the environment variable `GIT_EDITOR` is not set.

- `credential.helper`

    Specify an external helper to be called when a username or password credential is needed; the helper may consult external storage to avoid prompting the user for the credentials.
