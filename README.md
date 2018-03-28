# learn-conda

## conda

当强制vpn使用代理模式时，链接conda default可能会快一些（使用全局模式时，conda和pip要快的多，但网络不稳定，容易断线）

显示conda channel

    conda info
    conda config --get channels
    
The channels can be found in the .condarc file in your home directory.    

添加conda channel

    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --set show_channel_urls yes

使用特定的channel安装

    conda install -c defaults

删除特定的channel

    conda config --remove channels ...
    
[下载anaconda](https://www.anaconda.com/download)

[Installing on Linux 下载anaconda或者miniconda的安装文件](https://conda.io/docs/user-guide/install/linux.html)

[Installing on Windows 下载anaconda或者miniconda的安装文件](https://conda.io/docs/user-guide/install/windows.html)

在linux安装

用wget或者curl从上面的下载链接中把shell文件下载下来

    bash ~/Downloads/安装文件名

显示conda packages

    conda list
    
创建conda环境

    conda create -n py3 python=3
    conda create -n py2 python=2
    
## pip

    pip install tensorflow==1.0 -i https://pypi.mirrors.ustc.edu.cn/simple
    pip uninstall tensorflow
    
## git 

[Git installation instructions](https://www.udacity.com/wiki/ud775/install-git)

使用短行

如果文件包含很长的行，则会降低许多命令行工具（包括 Git）的实用性。 例如，如果使用 diff 比较两个将所有内容都放在同一行上的文件，则 diff 只会显示这两个文件是不同的文件，而无法指出哪里不同。

因此，在编写反思文件或其他纯文本文件时，确保每行长短适中是一种好做法。将行限制为多长是个人喜好问题。 许多开发者都将行限制为不超过 80 到 120 个字符。 有些编辑器能自动插入换行符，但在 Sublime 等其他编辑器中，如果想另起一行，请记得按下 Enter。

查看git版本

    git --version
    
在ubuntu中安装git

    apt-get install git
    sudo apt-get install git
    
For Ubuntu, this PPA provides the latest stable upstream Git version

    add-apt-repository ppa: git-core/ppa # apt update; apt install git
  
[git免密登录官方文档](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%87%AD%E8%AF%81%E5%AD%98%E5%82%A8#_credential_caching)

“store” 模式会将凭证用明文的形式存放在磁盘中，并且永不过期。 这意味着除非你修改了你在 Git 服务器上的密码，否则你永远不需要再次输入你的凭证信息。 这种方式的缺点是你的密码是用明文的方式存放在你的 home 目录下。

如果你使用的是 Mac，Git 还有一种 “osxkeychain” 模式，它会将凭证缓存到你系统用户的钥匙串中。 这种方式将凭证存放在磁盘中，并且永不过期，但是是被加密的，这种加密方式与存放 HTTPS 凭证以及 Safari 的自动填写是相同的。

Linux或者Mac下方法：

创建文件，进入文件，输入内容：

    cd ~
    touch .git-credentials
    vim .git-credentials
    https://{username}:{password}@github.com

在终端下输入：

    git config --global credential.helper store
    
打开~/.gitconfig文件，会发现多了一项:

    [credential]
    helper = store
    
如果使用的是gitlab，或者其他使用gitlab的代码管理平台，可以[使用sshkey来免密登录](http://blog.csdn.net/accountwcx/article/details/46822257)

列出与本地git或者某个git项目相关的信息，包括user email, user name, remote.origin.url等

    git config --list

## jupyter notebook

    jypyter notebook list

It will display all of the running servers on your machine.

在打开jupyter notebook时，当时在哪个目录下，打开的notebook的根目录就在哪个目录下。

## shell

在深度学习时代，需要用到GPU，而要对GPU进行控制，有两个选择，一是安装linux（不能是虚拟机，虚拟机没法很好的控制显卡），二是安装windows，在这种情况下，使用linux虚拟机的用户就需要直接在windows中控制GPU。

在windows中使用shell，有两种比较好的选择，一是使用Git Bash，如下所述，二是使用Anaconda Prompt，一般来说，两个都装，根据所要使用的shell命令的具体情况来选择。

[Command Line Instructions](https://www.udacity.com/wiki/ud775/command-line-instructions#!#windows-users)

windows: 使用Git Bash运行命令行

If you are on Windows, the native command prompt is a bit different from the ones you’d find on a Unix-based operating system like Ubuntu or Mac.  If you do not already have a more Unix-like command prompt installed, we highly recommend following the instructions on [this page](https://www.udacity.com/wiki/ud775/install-git/install-git-windows) to install Git.  You will need Git later in the course anyway, and it includes a Unix-like bash prompt called Git Bash that you can use to try out the tutorial linked above.

## pycharm

很好用的python IDE，甚至可以代替Sublime Text、Atom、Notepad++等编辑器

[Installing PyCharm on Linux](https://www.jetbrains.com/help/pycharm/requirements-installation-and-launching.html)

Unpack the <pycharm-professional or pycharm-community>-*.tar.gz file to a different folder, The recommended install location according to the filesystem hierarchy standard (FHS) is /opt.

    sudo tar xf <pycharm-professional or pycharm-community>-*.tar.gz -C /opt/pycharm

Switch to the bin directory:

    cd <new archive folder>/<pycharm-professional or pycharm-community>-*/bin
    
Starting PyCharm on Linux. Run pycharm.sh from the bin subdirectory.  

    ./pycharm.sh
