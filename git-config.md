`git config`是`git`的options，对`git`客户端进行全面的配置和定义，每个用户都会有属于自己的不同的config选项。

`config`有三个级别
- system 表示系统的全局配置
- global 表示用户的全局配置
- local  表示仓库的配置

从名称上来看，作用域从大到小，但优先级是从低到高，越贴近仓库的优先级越高。当配置项出现冲突时，优先级高的生效。

使用`list`参数可以看到全部配置项，如果需要查看作用域的配置，再加上具体作用域的参数，比如
```
$ git config --list --global    // 查看当前用户的global配置
```

`config`编辑有个很简单的办法，不需要记住那么多参数:
```
$ git config --global -e    // 编辑当前用户的global配置
```
如果需要更改其它作用域的参数，更换global为指定的即可，如果不加这个参数，默认是编辑当前仓库的config文件。这些不同作用域的配置的具体配置文件有哪些呢？ 可以通过`git help config`命令打开帮助查看，在FILES章节，但官方的帮助文档描述的并不详尽，不同OS的`git`客户端都有一些个性化的内容。

查看所有配置项时，可以通过添加--show-origin参数显示具体配置项属于哪个文件，你会发现config文件不是3个是4个。
[[/img/git-config/git_config_list_show_origin.png]]

#### system
这个文件一般都在/etc/gitconfig，优先级最低，对于windows用户在`git bash`里的路径是/mingw64/etc/gitconfig。

#### global
文件在~/.gitconfig这是用户使用最多的config文件，大多数的配置项都在这里配置。但这个作用域的配置文件有两个，另外一个是官方所说Second user-specific configuration file路径在$XDG_CONFIG_HOME/git/config，对于windows用户来说是%ProgramData%\git\config
这个配置文件官方的说法是这样的。
> Second user-specific configuration file. If $XDG_CONFIG_HOME is not set or empty, $HOME/.config/git/config will be used. Any single-valued variable set in this file will be overwritten by whatever is in ~/.gitconfig. It is a good idea not to create this file if you sometimes use older versions of Git, as support for this file was added fairly recently.

大致意思是这是第二个用户配置文件，如果$XDG_CONFIG_HOME不存在或为空，这个文件就是$HOME/.config/git/config, 这个配置文件中的任何单值变量都将被~/.gitconfig覆盖，该文件是最近才添加并被支持的。 那么在优先级上，肯定是~/.gitconfig更高一些。起初我不知道这个文件的存在，使用`git config --global --list`参看global配置项时，并不会load这个specific的配置文件，但使用`git config --list`时又load这个文件。

#### 自定义配置文件
global级别的配置文件是我使用做多自定义最多的配置文件，如果重装系统还要重新来过，所以我自己自定义了一个独立的config文件放在dropbox里，然后使用下面的命令`include`我的自定义文件到global配置文件。
```
$ git config --global include.path ~/dropbox/bak/.gitconfig
```

#### local
当前仓库的配置文件，.git/config没啥好说的，打开看看就全懂了。