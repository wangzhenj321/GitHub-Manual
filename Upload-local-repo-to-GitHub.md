## Question
How can I import source code from my computer to my GitHub account?

## Answer
If you've got local source code you want to add to a new remote new git repository without 'cloning' the remote first, do the following (I often do this - you create your remote empty repository in bitbucket/github, then push up your source).
1. Create the remote repository, and get the URL such as `git@github.com:/youruser/somename.git` or `https://github.com/youruser/somename.git`
If your local GIT repo is already set up, skips steps 2 and 3
2. Locally, at the root directory of your source, `git init`. (If you initialize the repo with a .gitignore and a README.md you should do a `git pull {url from step 1}` to ensure you don't commit files to source that you want to ignore.)
3. Locally, add and commit what you want in your initial repo (for everything, `git add .` then `git commit -m 'initial commit comment'`)
4. To attach your remote repo with the name 'origin' (like cloning would do) `git remote add origin [URL From Step 1]`
5. Execute `git pull origin master` to pull the remote branch so that they are in sync.
6. To push up your master branch (change master to something else for a different branch): `git push origin master`

## Notes
When you create the remote repository, don't choose "Initialize this repository with a README". Otherwise, you will get the following error.

![](img/Upload-local-repo-to-GitHub/git_push_rejected.png?raw=true)

## References
1. [import existing source code to github](https://stackoverflow.com/questions/4658606/import-existing-source-code-to-github)
