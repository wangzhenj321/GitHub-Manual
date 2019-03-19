## Description

Many Git commands take revision parameters as arguments. Depending on the command, they denote a specific commit or, for commands which walk the revision graph (such as `git log`), all commits which can be reached from that commit. In the latter case one can also specify a range of revisions explicitly.

In addition, some Git commands (such as `git show`) also take revision parameters which denote other objects than commits, e.g. blobs ("files") or trees ("directories of files").

## Specifying revisions

A revision parameter `<rev>` typically, but not necessarily, names a commit object. It uses what is called an extended SHA-1 syntax. Here are various ways to spell object names.

| Object names | Examples |
| --- | --- |
| `<sha1>` | dae86e1950b1277e545cee180551750029cfe735, dae86e |
| `<describeOutput>` | v1.7.4.2-679-g3bee7fb |
| `<refname>` | master, heads/master, refs/heads/master |
| `<refname>@{<date>}` | master@{yesterday}, HEAD@{5 minutes ago} |
| `<refname>@{<n>}` | master@{1} |
| `@{<n>}` | @{1} |
| `@{-<n>}` | @{-1} |
| `<branchname>@{upstream}` | master@{upstream}, @{u} |
| `<branchname>@{push}` | master@{push}, @{push} |
| `<rev>^` | HEAD^, v1.5.1^0 |
| `<rev>~<n>` | master~3 |
| `<rev>^{<type>}` | v0.99.8^{commit} |
| `<rev>^{}` | v0.99.8^{} |
| `<rev>^{/<text>}` | HEAD^{/fix nasty bug} |
| `:/<text>` | :/fix nasty bug |
| `<rev>:<path>` | HEAD:README, :README, master:./README |
| `:<n>:<path>` | :0:README, :README |
