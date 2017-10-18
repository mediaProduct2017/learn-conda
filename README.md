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
    