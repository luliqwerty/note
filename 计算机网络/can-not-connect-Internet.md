# 天塌了

我了个逗啊，我的这个网络真的是出了好多问题啊，之前寒假在家的那段时间就是B站有问题——所有的网络连接都没有问题就是B站不管是客户端还是网页都加载不出来。然后今天甚至我的浏览器都打不开了，在我多方搜索的情况下，算是了解到了一点皮毛（因为我还没学过计算机网络），**计算机网络真的是一门很重要的知识**。

## 很多问题都是代理问题

你记着，只要你的网络本身没问题，就肯定是代理出错了，首先想到是不是开了代理，VPN，还有看一下控制面板里的“网络和 Internet”选项中的局域网设置。

以下有两种我遇到的解决方案

1. 关闭所有代理（系统代理或者浏览器加载项里的而不是VPN代理，VPN就是靠代理才能访问到外网的）

2. 管理员权限下执行 `netsh winsock reset` 命令

   The `netsh winsock reset` command is used to reset the Winsock catalog back to its default state. This can help resolve network connectivity issues caused by corrupt or misconfigured Winsock settings.