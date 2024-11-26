# linux 中的环境变量

## 环境变量是什么

一串用冒号连接的文件目录，每次使用某些应用程序时都会优先在环境变量中查询，如果查询不到就报错，查到就运行。

example：gcc

```shell
$ gcc
实际上运行的是，简化命令行
$ /usr/bin/gcc
```



## 怎么添加环境变量

1. 临时，仅在当前命令行有效，一旦该命令行关闭即失效

    ```shell
    export PATH="PATH:what-you-need-to-add"
    ```

2. 对当前用户

    ```shell
    echo "export PATH=PATH:what-you-need-to-add"
    ```

3. 所有用户

    ```shell
    sudo echo "export PATH=PATH:what-you-need-to-add"
    ```

    