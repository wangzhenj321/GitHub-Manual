## Description

Create, list, delete or verify a tag object signed with GPG

## Synopsis

- `git tag <tagname> [<commit> | <object>]`
- `git tag -d <tagname>...`

## Examples

1. To push a single tag:
    
    ```
    git push origin <tag_name>
    ```
    
    And the following command should push all tags (**not recommended**):
    
    ```
    # not recommended
    git push --tags
    ```
