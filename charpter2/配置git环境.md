# 2.4 配置git环境

当安装完 Git 应该做的第一件事就是设置你的用户名称与邮件地址。 这样做很重要，因为每一个 Git 的提交都会使用这些信息，并且它会写入到你的每一次提交中，不可更改：

'''
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
'''

再次强调，如果使用了 --global 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git 都会使用那些信息。 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 --global 选项的命令来配置。

很多 GUI 工具都会在第一次运行时帮助你配置这些信息。

你也可以使用git config --list来查看git的所有配置。
