**vim 系统剪贴板**

**"+y 复制到系统剪切板**

**"+p 把系统粘贴板里的内容粘贴到vim**

 

在 Ubuntu 中使用VI/VIM时，发现无法使用系统的剪贴板。

上网一查，原来是少装了几个东西。

使用如下命令，安装相关的包。安装成功后，就可以使用系统剪贴板了。

 ```bash
sudo apt-get install vim vim-scripts vim-gtk vim-gnome
# 我在安装时显示 vim-gnome 一下信息
# Package vim-gnome is not available, but is referred to by another package.This may mean that the package is missing, has been obsoleted, or is only available from another source
 ```


使用如下命令查看：

```bash
vim --version | grep clipboard
```

注意 **clipboard** 和 **xterm_clipboard** 前面的 **加号（ +）** 。

加号（+），表示支持；

减号（-），表示不支持。