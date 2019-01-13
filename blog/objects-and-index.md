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

There are three areas where file changes can reside from git’s point of view: **working directory**, **staging area**, and **the repository**.

![](../img/objects-and-index/git_index_1.png?raw=true)

When you work on your project making changes you are dealing with your project’s **working directory**. **This is the project directory on your computer’s filesystem.** All the changes you make will remain in the working directory until you add them to the **staging area** (via `git add` command). The staging area is best described as a preview of your next commit. Meaning, when you do a git commit, git will take the changes that are in the staging area and make the new commit out of those changes. One practical use of the staging area is that it allows you to fine-tune your commits. You can add and remove changes from staging area until you are satisfied with how your next commit will look like, at which point you can do `git commit`. And after you commit your changes they go into `.git/objects` directory where they are saved as *commit*, *blob* and *tree* objects.

Although it is often useful to think of staging area as some real area (or directory) where git stores changes (like it does in `.git/objects` ) this is not entirely true. **Git doesn’t have a dedicated staging directory where it puts some objects representing file changes (blobs). Instead, git has a file called the index that it uses to keep track of the file changes over the three areas: working directory, staging area, and repository.** And when you add changes to your staging area, git updates the information in the index about those changes and creates new blob objects, but puts them in the same `.git/objects` directory with all the other blobs that belong to previous commits. This maybe sounds a bit complicated but actually it isn’t, so let’s go through a typical git workflow example to display how git uses the index.

- Step 1: `git checkout`

- Step 2: editing working directory

- Step 3: `git add`

- Step 4: `git commit`

### `git checkout`

Let’s say we are on a `master` branch and there is also a `feature` branch in our repository. If we do

```
git checkout feature
```

three things are going to happen.

1. git will move the `HEAD` pointer to point to the `feature` ref (branch). To make things more simple we will display only the last commit on the `feature` branch.

    ![](../img/objects-and-index/git_index_2.png?raw=true)

2. git will take the content of the commit that `feature` is pointing to and add it to the index.

    ![](../img/objects-and-index/git_index_3.png?raw=true)
    
    As we mentioned earlier index is not a directory but a file, so git is not actually storing objects (blobs) into it. Instead, git is storing information about each file in our repository:

    - `mtime` :  is the time of last update
    
    - `file`: name of the file
    
    - `wdir`: file version in working directory
    
    - `stage`: file version in the index
    
    - `repo`:  file version in the repository
    
    File versions are marked with checksums (if two files have the same checksum then they have the same content/version).

3. git will make your working directory match the content of the commit that `HEAD` is pointing to (it will recreate the content of your project’s directory using tree and blob objects).

    ![](../img/objects-and-index/git_index_4.png?raw=true)

So, after checkout, every file will have the same version in the working directory, staging area/index, and the repository.

### editing working directory

If we now edit our `index.php` file

![](../img/objects-and-index/git_index_5.png?raw=true)

those changes will affect only our working directory. But if we now run

```
git status
```

git will first update the index with the new working directory version for `index.php`

![](../img/objects-and-index/git_index_6.png?raw=true)

and then it will see that `index.php` has different versions in working and staging directory.

![](../img/objects-and-index/git_index_7.png?raw=true)

So, git will tell us

```
On branch feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
modified:   index.php
no changes added to commit (use "git add" and/or "git commit -a")
```

that there are changes in our working directory which are not in our staging area (and therefore won’t be included in our next commit at this point).

### `git add`

So let’s add our `index.php` file to the staging area by doing

```
git add index.php
```

Two things are going to happen. First, git will create a blob object for our `index.php` file and store it into `.git/objects` directory and second, it will again update the index.

![](../img/objects-and-index/git_index_8.png?raw=true)

If we now do

```
git status
```

git will see that `index.php` version in staging area matches the working directory version but doesn’t match the repository version

![](../img/objects-and-index/git_index_9.png?raw=true)

so git will tell us:

```
On branch feature
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
modified:   index.php
```

that `index.php` is now staged to be committed.

### `git commit

And now when we commit our changes

```
git commit -m "Adding some code magic to index.php"
```

git will:

1. create a new commit object and tree object (and hook them up with the blob object that was already created with `git add`)

2. move the `feature` ref pointer to the new commit

3. update the index.

![](../img/objects-and-index/git_index_10.png?raw=true)

And now our `index.php` file again contains the same versions in all git areas.

### References

1. [Understanding Git — Index](https://hackernoon.com/understanding-git-index-4821a0765cf)
