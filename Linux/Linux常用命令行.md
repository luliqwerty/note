## Linux常用命令行

## 用到了就放进来没必要直接看所有的命令

## 需求和兴趣才是学习的目的

告诫 ：在 Linux 下 rm 命令慎用

建议 ：把所有想删除的文件用 mv 操作移动到 /trash（自定义的回收站） 之后统一清除。

### ls  -  list

```bash
# ls 默认是当前文件路径 也可以加路径输出其它文件夹的子项
# all 输出所有文件、文件夹（包括隐藏文件）
	ls -a
# list 以完整的形式列出
	ls -l
# 以易读的形式输出
	ls -h
# 组合参数
	ls -ahl
```

### cd  -  change directory

```bash
cd [文件目录]
cd / 进入根目录
cd ..  返回上一级目录

cd - # 进入上一次的目录
# 当前在 / 目录下
# 使用命令 cd /~/Desktop/code/C
# 再使用 cd - 直接返回 / 目录
```

### root 账户

Linux 很多骚操作必须在 root 下才能进行

```bash
# 设置 root 密码
sudo passwd root

# 某些操作提示权限不够时直接在之前添加 sudo
注意 sudo 和 super manager 不一样 sudo 仅仅操作当前root账户 super manager 是整个系统
# 进入 root 账户
1. su -
2. 输入密码

# Linux 好用的就是环境配置极其容易
sudo apt-get install [软件包]
```

### pwd  -  print current working directory

```bash
pwd
home/lucky/note
```

### mkdir  -  make directory

```bash
1. mkdir 路径
	# 在上一级目录下的 bin 文件夹下创建目录 mydir
	mkdir ../bin mydir

2. mkdir -p 路径
	# 一次性创建多层不存在的目录
	mkdir -p a/b/c
	# 能直接创建出3层文件夹 可以用 tree 查看

3. mkdir 路径1 路径2
	mkdir a b c
	# 在当前目录下创建3个目录 a b c
```

### rm  -  remove

```bash
1. 删除文件
	# 删除文件
	rm file
	# 删除usr路径下的file
	rm /usr/file
2. 删除目录
	# 删除文件夹
	rm -rf /usr/directory
```

### apt-get / apt

```bash
# 卸载软件
sudo apt-get --purge remove [package]
```

### touch  -  创建新文件

```bash
1. touch 路径
	# 创建 linux.txt 文件
	touch linux.txt
	# 在上一级目录下新建 linux 文件
	touch ../linux

2. touch 路径1 路径2
	# 在当前路径创建 file 和 file.txt
	touch file file.txt
```

### cp  -  copy files or directories

```bash
1. 复制文件
	# cp [被复制的文件路径] [目标路径]
	# 把 /home/lucky/note/firstNote.md 复制到 根目录/ 去
	cp /home/lucky/note/firstNote.md /
2. 复制文件夹
	# cp -r [被复制的文件夹路径] [目标路径]
	# 把 /home/lucky/note 文件夹 复制到 根目录/ 去
	cp -r /home/lucky/note /
	cp -r ./swapClass ./learnCmake
```

### mv  -  move(rename) files

```bash
1. 移动文件
	mv 路径1(具体到那个文件/文件夹) 路径2
2. 重命名文件
	mv 路径/filenane （相同）路径/filename_changed
```

### man  -  an interface to the system reference manuals

作用： 包含了Linux中全部命令手册 用于查看命令使用手册， 按q退出

```bash
# 查看 ls 命令使用
	man ls
# 查看 cd 命令使用
	man cd
# 查看 man 命令使用
	man man
```

### reboot  -  reboot the machine

```bash
# 立即重启机器
	reboot
```

### shutdown -  power-off the machine

作用：关机  shutdown -h [时间]

```bash
# 立即关机
	shutdown -h now
```

### ping

```bash
# 查看是否能连接到某网站的服务器，能拿到数据则说明不是网络问题
# ping host
ping baidu.com
ping google.com
```

### chmod - change mod

```bash

```

### mount
```bash

```
### ip / ifconfig

```bash
# 获取本机IP
ip address(a)

# ifconfig is a outdated command
```

### tar 归档和解档

```bash
-c 创建一个新归档
-x 从归档中解出文件
-v 详细列出处理的文件
-f 使用归档文件
-z 使用 gzip 进行归档

# 常用命令选项
tar [选项] [压缩包名称] [被压缩文件目录]
# 压缩：
tar -zcvf filename.tar ~/Desktop/
# 解压缩：
tar -zxvf filename.tar.gz
```

### free

```bash
free -h
# 检查可用内存
```

### df

```bash
# 查看磁盘空间
df -lh
```

### find

```bash

```

## grep

```bash
# 在某个文件中查询 text
grep "text" file_name

# 递归搜索当前目录下所有文件，将打印所有含有 text 的行
grep "text" . -r -n
grep "text" directory -r -n
```

### jobs

```bash

```

### ps process(进程)

```bash

```

### netstat

```bash

```

