# 2.1在Linux上安装Git

安装命令如下：
'''
sudo apt-get install git
'''
安装完成后，输入"git --version"查看git版本，如果出现“git version x.x.x”证明安装成功。

题外话：老一点的Debian或Ubuntu Linux，要把命令改为sudo apt-get install git-core，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。

