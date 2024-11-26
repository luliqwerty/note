起因：我在做龙芯班布置的 OS 作业时想着使用以下 wsl + visual studio code 来做作业，然后发现 clone 不了作业仓库，我就发现不对了，然后就开始疯狂的 `ping` 中

```bash
ping baidu.com
ping github.com
ping help.ubuntu.com
```
结果如下：

[![image-20241021174410213.png](https://i.postimg.cc/8z1bCzkk/image-20241021174410213.png)](https://postimg.cc/qz5Kb0CW)

再然后肯定就是疯狂的查询资料解决问题

[CSDN小肠文](https://blog.csdn.net/uouj3766/article/details/126596459) 等等等

搜索得到的所有的解决方案如下

1. `ifconfig`

    众所周知，我是刚下载的 wsl，哪来的 `ifconfig` 呢？所以这当然对我没用。

2. `ip route`

    这个命令我看他们都有输出结果，为什么我的没有呢？然后就也解决不了我的问题啊。

痛痛痛死我了

然后我知道为什么突发奇想想着要不要重启一下 虚拟机平台 和 适用于 Linux 的 Windows 子系统 这两个 Windows 功能呢？然后就好了，是不是很逆天，我也这样觉得！！！

问大佬，大佬回答如下

https://github.com/microsoft/WSL/issues/10709#issuecomment-2159629182 可能还有后遗症，似乎是VMware有冲突。问题复发的话看这个

(大佬查问题都是从源头开始找，而我从 `CSDN` 找，向佬学习)