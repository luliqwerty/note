## VmwareNATservices占用CPU过高的情况

- 问题描述：

  - 虚拟机关闭后 VMware NAT service 占用CPU过高导致风扇嘎吱装，但直接在任务管理器关闭 VMware NAT service 进程会导致下次打开虚拟机虚拟机不能联网的问题。

- 解决方案：

  - ```bash
    win + r
    输入 services.msc 进入 本地服务
    找到 VMware NAT service 
    重启该项
    ```

问题解决了 写代码真是一件令人高兴的事情。