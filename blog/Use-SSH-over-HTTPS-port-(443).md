
***

最近几天我这里出现了`git push`出现 timeout 的问题：
```
$ git push
ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
在Github官网找到了一种办法，通过https协议建立SSH连接，即让SSH走443端口。经过测试，公司的防火墙并没有封443端口（基本不可能封）。

***

Sometimes, firewalls refuse to allow SSH connections entirely. If using HTTPS cloning with credential caching is not an option, you can attempt to clone using an SSH connection made over the HTTPS port (443). Most firewall rules should allow this, but proxy servers may interfere.

To test if SSH over the HTTPS port is possible, run this SSH command:
```
$ ssh -T -p 443 git@ssh.github.com
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```

## Enabling SSH connections over HTTPS

If you are able to SSH into `git@ssh.github.com` over port 443, you can override your SSH settings to force any connection to GitHub to run through that server and port.

To set this in your ssh config, edit the file at `~/.ssh/config`, and add this section:
```
Host github.com
  Hostname ssh.github.com
  Port 443
```
You can test that this works by connecting once more to GitHub:
```
$ ssh -T git@github.com
Hi username! You've successfully authenticated, but GitHub does not
provide shell access.
```

> **Tips**
You must set the `Host` names as `github.com`, because the host name is `github.com` while cloning with SSH.

## References
1. [SSH走443端口访问github](http://www.51201314.me/jacks/zh-Hans/2016/11/07/SSH%E8%B5%B0443%E7%AB%AF%E5%8F%A3%E8%AE%BF%E9%97%AEgithub/)
2. [改用 443 端口连接 Github 修复 git push 时出现 Connection timed out 的问题](https://mozillazg.github.io/2015/08/use-443-port-fix-github-connection-timeout.html#)
3. [Using SSH over the HTTPS port](https://help.github.com/articles/using-ssh-over-the-https-port/)