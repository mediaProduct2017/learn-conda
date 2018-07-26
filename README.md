# learn-conda

## conda

Anaconda是发行版，如果对anaconda自带的常用包，UI，IDE不感兴趣的话可以安装miniconda。

conda可以安装不同版本的python，同理也可以安装不同版本的其他软件。

当强制vpn使用代理模式时，链接conda default可能会快一些（使用全局模式时，conda和pip要快的多，但网络不稳定，容易断线）

显示conda channel

    conda info
    conda config --get channels
    
The channels can be found in the .condarc file in your home directory.    

添加conda channel

    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --set show_channel_urls yes
    
[清华的conda下载镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)
   
[科大的conda下载镜像](https://mirrors.ustc.edu.cn/anaconda/archive/)
    
[科大Anaconda 源使用帮助](https://mirrors.ustc.edu.cn/help/anaconda.html)

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
    
创建conda环境，不同环境安装不同的某个软件，比如cuda, 不一定是不同的python

    conda create -n env_name
    
创建conda环境，不同环境安装不同的python

    conda create -n py3 python=3
    conda create -n py2 python=2
    
删除conda环境

    conda env remove -n <env_name>
    conda env remove -n tensorflow
    
列出所有的conda环境

    conda env list
    conda env list --json
    
    conda info --env
    
在linux或者mac中，进入虚拟环境可以

    source activate py3
    conda activate py3
    
在windows中，进入虚拟环境可以

    activate py3
    
有时候在windows中，在terminal中deactivate之后，activate命令就不能用了，必须新开一个terminal才能用activate.

conda本质上是管理系统中的环境变量，软件装在哪里其实并不重要。软件装在envs中的好处是当虚拟环境删除时，软件也自然被删掉。另外，python等软件是可以用conda自动安装的，自动安装在envs中，并自动配置所需要的环境变量。

在conda中手动配置某些环境变量

Anaconda can run any bash scripts each time when the environment is activated. Such scripts should be placed in the following path:

    /<path to anaconda>/envs/<env name>/etc/conda/activate.d/
    
Here is how we can create an executable script that will be executed by Anaconda each time when the environment is activated by user:

    mkdir -p ~/anaconda3/envs/tf_cu90/etc/conda/activate.d
    touch ~/anaconda3/envs/tf_cu90/etc/conda/activate.d/activate.sh
    vim ~/anaconda3/envs/tf_cu90/etc/conda/activate.d/activate.sh
    chmod +x ~/anaconda3/envs/tf_cu90/etc/conda/activate.d/activate.sh
    
在具体的虚拟环境中，etc/conda/activate.d这个目录比一定存在，所以需要创建目录

And 2 simple commands that should be in the shell script:

    #!/bin/sh
    ORIGINAL_LD_LIBRARY_PATH=$LD_LIBRARY_PATH
    export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:/usr/local/cuda-9.0/extras/CUPTI/lib64:/lib/nccl/cuda-9:$LD_LIBRARY_PATH

We are doing 2 things here:

saving original value of the LD_LIBRARY_PATH (we will need it later)

updating LD_LIBRARY_PATH (so it includes reference to the cuda9.0)

This should be almost enough to make our environment working with CUDA9.0. After re-activating the environment you should be able to use TF 1.5.0 with the CUDA9.0

However, there is something we still need to do. The thing is that if you deactivate the environment, your LD_LIBRARY_PATH value remains

In order to avoid, we do need to set LD_LIBRARY_PATH to the old value that it had before the environment was activated. To do so we need to create another file. Surprise-surprise, since Anaconda has the ability to run any script during the activation phase, it can do the same during the de-activations phase. You just need to put your script here:

    /<path to conda>/envs/<env name>/etc/conda/deactivate.d/
    
Let’s do it:

    mkdir -p ~/anaconda3/envs/tf_cu90/etc/conda/deactivate.d
    touch ~/anaconda3/envs/tf_cu90/etc/conda/deactivate.d/deactivate.sh
    vim ~/anaconda3/envs/tf_cu90/etc/conda/deactivate.d/deactivate.sh
    chmod +x ~/anaconda3/envs/tf_cu90/etc/conda/deactivate.d/deactivate.sh

and, as you have probably guessed here is what we’re going to put inside:

    #!/bin/sh

    export LD_LIBRARY_PATH=$ORIGINAL_LD_LIBRARY_PATH
    unset ORIGINAL_LD_LIBRARY_PATH


## pip

    pip install tensorflow-gpu==1.0 -i https://pypi.mirrors.ustc.edu.cn/simple
    pip uninstall tensorflow-gpu
    
## git 

[nlp/nlp_models/git](https://github.com/arfu2016/nlp/tree/master/nlp_models/git)

[Git installation instructions](https://www.udacity.com/wiki/ud775/install-git)

[git windows](https://gitforwindows.org/)

In mac, git comes with xcode.

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

## linux安装

在windows中用虚拟机安装linux，可以用vmvare, virtual box或者docker

## shell

-之后一般是单个字母，--之后一般是英文单词

在深度学习时代，需要用到GPU，而要对GPU进行控制，有两个选择，一是安装linux（不能是虚拟机，虚拟机没法很好的控制显卡），二是安装windows，在这种情况下，使用linux虚拟机的用户就需要直接在windows中控制GPU。

在windows中使用shell，有两种比较好的选择，一是使用Git Bash，如下所述，二是使用Anaconda Prompt，一般来说，两个都装，根据所要使用的shell命令的具体情况来选择。在Git Bash中，mkdir, ls, cd等都能使用。在Anaconda Prompt中，只能使用conda, python, cd等。Git Bash是bash，所以可以使用大部分bash命令，而Anaconda Prompt并不是bash，所以只能选择性的用一些linux命令。

在windows中，还可以搜索运行，然后在运行中搜索cmd，可以得到一个terminal，用这个terminal进入相应的文件夹（使用cd），然后就可以调用其中的exe文件（直接写文件名执行）。

[Command Line Instructions](https://www.udacity.com/wiki/ud775/command-line-instructions#!#windows-users)

windows: 使用Git Bash运行命令行

If you are on Windows, the native command prompt is a bit different from the ones you’d find on a Unix-based operating system like Ubuntu or Mac.  If you do not already have a more Unix-like command prompt installed, we highly recommend following the instructions on [this page](https://www.udacity.com/wiki/ud775/install-git/install-git-windows) to install Git.  You will need Git later in the course anyway, and it includes a Unix-like bash prompt called Git Bash that you can use to try out the tutorial linked above.

linux中的查找命令

find，比如以下是在当前目录及其子目录搜索cuda文件或者以cuda开头的文件

    find . -name 'cuda'
    find . -name 'cuda*'

locate，是find -name的另一种写法，但比后者快得多，它不搜索具体目录，而是搜索一个数据库。这个数据库每天自动更新一次，所以用locate找不到最新变动过的文件。需要使用updatedb手动更新数据库。

找的是文件的开头

whereis，只能用于程序名的搜索。

which，搜索执行的是哪个位置的命令。

[Linux的五个查找命令](http://www.ruanyifeng.com/blog/2009/10/5_ways_to_search_for_files_using_the_terminal.html)

## pycharm

很好用的python IDE，甚至可以代替Sublime Text、Atom、Notepad++等编辑器

[Installing PyCharm on Linux](https://www.jetbrains.com/help/pycharm/requirements-installation-and-launching.html)

Unpack the \<pycharm-professional or pycharm-community>-*.tar.gz file to a different folder, The recommended install location according to the filesystem hierarchy standard (FHS) is /opt.

    sudo tar xf <pycharm-professional or pycharm-community>-*.tar.gz -C /opt/pycharm

Switch to the bin directory:

    cd <new archive folder>/<pycharm-professional or pycharm-community>-*/bin
    
Starting PyCharm on Linux. Run pycharm.sh from the bin subdirectory.  

    ./pycharm.sh
    
给pycharm设置主题颜色

editor:

settings - Editor - Color Scheme, 可以选择General，也可以选择具体的语言

下面的terminal：

settings - Editor - Color Scheme, 选择Console Font和Console Colors

左边的sidebar和project view:

settings - Appearance and Behavior - Appearance - UI options - Theme.

## crontab

[crontab](https://github.com/arfu2016/nlp/tree/master/nlp_models/crontab)

## github

修改系统hosts文件的办法，绕过国内dns解析，直接访问GitHub的CDN节点，从而达到加速的目的。不需要科学上网，也不需要海外的服务器辅助。

1 获取GitHub官方CDN地址  
打开https://www.ipaddress.com/

查询以下三个链接的DNS解析地址     
1. github.com   
2. assets-cdn.github.com   
3. github.global.ssl.fastly.net  

记录下查询到的IP地址。

2018.7.26的记录为：

192.30.253.112 github.com  
151.101.184.133 assets-cdn.github.com  
151.101.185.194 github.global.ssl.fastly.net  

2 修改系统Hosts文件

sudo vim /etc/hosts

在末尾添加三行记录并保存。(需管理员权限，注意IP地址与域名间需留有空格)

i ctrl+c ctrl+v esc :wq

3 有可能需要刷新机器上的dns缓存（本次不需要）

Tiger或更低版本 Mac OS：sudo lookupd -flushcache  
Leopard和Snow Leopard：sudo dscacheutil -flushcache  
Lion、Mountain Lion和Mavericks：sudo killall -HUP mDNSResponder  
Yosemite:sudo discoveryutil mdnsflushcache  

这几个命令有可能都要测试下，哪个有效就用哪个。

[加速国内Github访问](https://blog.csdn.net/w958660278/article/details/81161224)

[Mac下修改hosts 解决访问github慢的问题](https://blog.csdn.net/cjopengler/article/details/45603171)

[Mac OS X EI Capitan清空DNS缓存](https://blog.csdn.net/lwjdgl/article/details/50274285)

