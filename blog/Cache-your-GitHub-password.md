If you're cloning GitHub repositories using HTTPS, you can use a credential helper to tell Git to remember your GitHub username and password every time it talks to GitHub.

If you clone GitHub repositories using SSH, then you authenticate using SSH keys instead of a username and password. For help setting up an SSH connection, see Generating an SSH Key.

> **Tips:**
> 
> 1. You need Git 1.7.10 or newer to use the osxkeychain credential helper.
> 2. If you installed Git using Homebrew, the *osxkeychain helper* will already be installed.
> 3. If you're running Mac OS X 10.7 and above and you installed Git through Apple's Xcode Command Line Tools, then *osxkeychain helper* is automatically included in your Git installation.

Install Git and the *osxkeychain helper* and tell Git to use it.

1. Find out if Git and the *osxkeychain helper* are already installed:
```
$ git credential-osxkeychain
# Test for the cred helper
Usage: git credential-osxkeychain <get|store|erase>
```

2. If the *osxkeychain helper* isn't installed and you're running OS X version 10.9 or above, your computer will prompt you to download it as a part of the Xcode Command Line Tools:
```
$ git credential-osxkeychain
xcode-select: note: no developer tools were found at '/Applications/Xcode.app',
requesting install. Choose an option in the dialog to download the command line developer tools.
```
Alternatively, you can install Git and the *osxkeychain helper* by using Homebrew:
```
$ brew install git
```

3. Tell Git to use *osxkeychain helper* using the global credential.helper config:
```
$ git config --global credential.helper osxkeychain
# Set git to use the osxkeychain credential helper
```

The next time you clone an HTTPS URL that requires a password, you'll be prompted for your username and password, and to grant access to the OSX keychain. After you've done this, the username and password are stored in your keychain and you won't be required to type them in to Git again.

## References
1. [Caching your GitHub password in Git](https://help.github.com/articles/caching-your-github-password-in-git/#platform-mac)