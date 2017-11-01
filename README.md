# learn-conda

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
    
在ubuntu中安装git

    apt-get install git
    sudo apt-get install git
    
For Ubuntu, this PPA provides the latest stable upstream Git version

    add-apt-repository ppa: git-core/ppa # apt update; apt install git
    