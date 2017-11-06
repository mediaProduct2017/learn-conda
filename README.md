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

在linux安装

    bash ~/Downloads/安装文件名

显示conda packages

    conda list
    
创建conda环境

    conda create -n py3 python=3
    conda create -n py2 python=2
    
## git    
    
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

## pycharm

[Installing PyCharm on Linux](https://www.jetbrains.com/help/pycharm/requirements-installation-and-launching.html)

Unpack the <pycharm-professional or pycharm-community>-*.tar.gz file to a different folder, The recommended install location according to the filesystem hierarchy standard (FHS) is /opt.

    sudo tar xf <pycharm-professional or pycharm-community>-*.tar.gz -C /opt/pycharm

Switch to the bin directory:

    cd <new archive folder>/<pycharm-professional or pycharm-community>-*/bin
    
Starting PyCharm on Linux. Run pycharm.sh from the bin subdirectory.  

    ./pycharm.sh
    
    