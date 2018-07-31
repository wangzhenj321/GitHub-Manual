Tracking the development process of a project in detail is very important to push the project forward until the end of successful accomplishment. The “issue -> pull request -> merge” cycle will be used on GitHub to track our development and maintain the projects. 

The “issue” step is for project managers to organize tasks, such as adding new features, reporting software bugs, and auditing old accomplished functionality [About issues](https://help.github.com/articles/about-issues/).

With the function of notification, members will receive the up-to-date tasks which released by managers through “issue”. Then you can start your task according to the description in the “issue”, or you can discuss with managers by writing comments under the “issue” if you have any confusion about the content of the “issue”. Once you made clear of the task, it’s time to start the “pull request” step, and you’ll need to fork the repository to your own GitHub account, clone the forked repository to your local machine, accomplish the task described in the “issue”, push the changes back to your GitHub account, and finally send a pull request to accomplish the “pull request” step [About pull requests](https://help.github.com/articles/about-pull-requests/).

Managers will receive the notification for your pull request. Through testing your code, managers can either write comments to inquire with further improvement or merge your pull request to end this “issue”. It’s also possible to close a pull request to reject the changes [About pull request merges](https://help.github.com/articles/about-pull-request-merges/).

The “issue -> pull request -> merge” cycle has been conceptually descried as above, and then you can refer to the following sections to implement this cycle in practice. The Section "Basic settings for Git" describes few basic settings for Git in your local machine, which you only need to do once time. Other sections describe three steps of the “issue -> pull request -> merge” cycle, respectively.

![](img/Issue-to-Pull-Request-to-Merge/git_basic_workflow.png?raw=true)

#### Table of Contents
[Basic settings for Git](#basic-settings-for-git)

[Releasing an Issue](#releasing-an-issue)

[Creating a Fork](#creating-a-fork)

[Keeping your local repository up-to-date](#keeping-your-local-repository-up-to-date)

[Starting your work by creating a branch](#starting-your-work-by-creating-a-branch)

[Cleaning up your work](#cleaning-up-your-work)

[Submitting a Pull Request](#submitting-a-pull-request)

[Merging a Pull Request](#merging-a-pull-request)

[Keywords for closing issue](#keywords-for-closing-issue)

[References](#references)

## Basic settings for Git
If you finished these settings, it will be easier to understand who makes the commits from committing logs for your coauthors.

```
$ git config --global user.name "Your Name"          // Setting of your name

$ git config --global user.email YourEmailAddress    // Setting of your email

$ git config --global color.ui true                  // Setting of display color

$ git config -l                                      // Confirm the settings
```

![](img/Issue-to-Pull-Request-to-Merge/git_log.png?raw=true)

The following command is also recommended to set up Sublime Text as Git message editor.

**On Windows 10**

```
$ git config --global core.editor "'C:\Program Files\Sublime Text 3\subl.exe' -w"
```

If you want to open the Sublime Text from the command line, you need to add the path of Sublime Text into your PATH. Once you've added, the command `subl.exe` can be used to open up Sublime Text.

**On Mac OS**

You first need to add the path of Sublime Text into your PATH.

```
git config --global core.editor "subl -n -w"
```

## Releasing an Issue
[Mastering Issues](https://guides.github.com/features/issues/)

## Creating a Fork
After received notification of “issue” from managers, please follow the next sections to implement the task of “issue” to finish the “pull request” step. Sign in the GitHub, find the repository that you want to fork. Click the “Fork” button at the upper right corner. 

![](img/Issue-to-Pull-Request-to-Merge/fork_button.png?raw=true)

Once you’ve done that, you can find that repository in your account and clone it to your local machine.

![](img/Issue-to-Pull-Request-to-Merge/https_url_for_clone.png?raw=true)

In order to clone the fork to your local machine, copy the HTTPS URL from the list of “Clone or download” and use the following command.

```
$ git clone https://github.com/wangzhen-Geosurf/SandBox.git    // Clone your fork to your local machine
```

After you finished cloning the repository, you can verify the new remote named as “origin”.

```
$ git remote -v                                                // Verify the new remote named as “origin”
```

![](img/Issue-to-Pull-Request-to-Merge/git_remote_origin.png?raw=true)

In order to make sure you keep the repository up to date, you should track the original “upstream” repository from where you forked. To do this, you will need to add a new remote.

```
$ git remote add upstream https://github.com/geosurf-dev/SandBox.git    // Add “upstream” repository to list of remotes

$ git remote -v                                                         // Verify the new remote named as “upstream”
```

![](img/Issue-to-Pull-Request-to-Merge/git_remote_upstream.png?raw=true)

## Keeping your local repository up-to-date
Whenever you want to update the repository by merging the upstream changes, you will need to fetch the upstream and merge it. 

```
$ git fetch upstream                    // Fetch upstream remote to update the upstream/master branch

$ git checkout master                   // Checkout your master branch

$ git merge upstream/master             // Merge with upstream/master branch
```

## Starting your work by creating a branch
Whenever you begin work on a new feature or bugfix, you will need to create a new branch.

```
$ git checkout master                   // Checkout the branch where you want to start your new branch

$ git branch TestPullRequest              // Create a new branch named as TestPullRequest

$ git checkout TestPullRequest            // Switch to your new branch to start your work
```

Now, you can go ahead to make changes you want to. Once you finished your changes, you’ll need to input the following commands to commit your changes.

```
$ git status                            // Show the modified files in working directory

$ git add FileName                      // Stage the modified files for commit

$ git status                            // Confirm the modified files been added for commit

$ git commit -m "commit message"        // Commit the changes

$ git status                            // Confirm the changes been committed
```

## Cleaning up your work
Before submitting your pull request, you should rebase your development branch based on the last upstream to make sure that merging your code will not trigger any conflict. Before rebasing your development branch, you’ll need to update the master branch by merging with the upstream remote. Please refer to Section “Keeping your local repository up-to-date” to do it.

```
$ git checkout TestPullRequest          // If there were any new commits, rebase your development branch

$ git rebase master                     // Merge any new commits in upstream into your development branch
```

Once you finished the previous process, you can push your changes to your GitHub account.

```
$ git push origin HEAD                  // Push commits to origin
```

![](img/Issue-to-Pull-Request-to-Merge/git_push_origin_HEAD.png?raw=true)

## Submitting a Pull Request
Once you’ve pushed all of your changes to your GitHub account (origin), go to the page of that fork on your GitHub, and click the “Pull Request” to create a pull request. While creating a pull request, be careful to select the “base fork”, “base”, “head fork” and “compare”. After you sent the “Pull Request”, it’s always possible to get comments from managers to ask for some improvement. When you need to make any changes to your pull request based on managers’ comments, just push the updates to GitHub (origin). Your pull request will automatically track the changes on your development branch.

![](img/Issue-to-Pull-Request-to-Merge/create_pull_request.png?raw=true)

## Merging a Pull Request
[Merging a pull request](https://help.github.com/articles/merging-a-pull-request/)

## Keywords for closing issue
Please refer to the following link [Closing issues using keywords](https://help.github.com/articles/closing-issues-using-keywords/) to learn how to use keywords to automatically close issues. And please be careful to the following two points I want to emphasize, while you reading the link.
- One is that these nine keywords have same function, so you can choose anyone you like.
- Another is that while closing multiple issues, please preface each issue reference with one of the above keywords. The usage of attaching more than one issue reference with only one keyword, which you can find on internet, is possible to trigger error.

## References
1. [GitHub Standard Fork & Pull Request Workflow](https://gist.github.com/Chaser324/ce0505fbed06b947d962)
