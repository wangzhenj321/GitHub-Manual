## Part 1: Objects

### The SHA

All the information needed to represent the history of a project is stored in files referenced by a 40-digit **object name** that looks something like this `6ff87c4664981e4397625791c8ea3bbb5f2279a3`. You will see these 40-character strings all over the place in Git. In each case the name is calculated by taking the SHA1 hash of the contents of the object. The SHA1 hash is a cryptographic hash function. What that means to us is that it is virtually impossible to find two different objects with the same name.

### Objects

Every object consists of three things: **type**, **size** and **content**. The **size** is simply the size of the contents, the **content**s depend on what type of object it is, and there are four different types of objects: **blob**, **tree**, **commit**, and **tag**.

1. **blob** is used to store file data. ***It is generally a file.***

2. **tree** is basically like a directory. ***It references a bunch of other trees and/or blobs (i.e. files and sub-directories).***

3. **commit** ***points to a single tree, marking it as what the project looked like at a certain point in time.*** It contains meta-information about that point in time, such as a timestamp, the author of the changes since the last commit, a pointer to the previous commit(s), etc.

4. **tag** is a way to ***mark a specific commit as special*** in some way. It is normally used to tag certain commits as specific releases or something along those lines.

Almost all of Git is built around manipulating this simple structure of four different object types. It is sort of its own little filesystem that sits on top of your machine's filesystem.

### Example

1. Create a simple local repository, including two files of `index.cpp` and `README.md` and a dummy commit, shown as the following figure. And the name of **commit object** is `efec32c221f1838a793a0a9e1aee9ef36781d962`.

    ![](../img/objects-and-index/dummy_repo.png?raw=true)

2. Show all the objects.

    ![](../img/objects-and-index/all_objects.png?raw=true)

3. Figure out the structure of these objects by using `cat-file`. The **commit object** points to a single **tree object** of `f424da40484f3e6ca7f761b2a4a8645e61a2c7e2`, and this single tree includes two **blob object** of `5e14e87c708df99e9e3cfdb7c3ad7aee2aee7a98` and `d5a7322872f1ae27c4e31f48f7ec1dc64a7359a4`.

    ![](../img/objects-and-index/structure_of_objects.png?raw=true)

### References

1. [The Git Object Model](http://shafiulazam.com/gitbook/1_the_git_object_model.html)

## Part 2: Index

### References

1. [Understanding Git — Index](https://hackernoon.com/understanding-git-index-4821a0765cf)
