# 编译器GCC

## 1. 编译器，调试器安装

```bash
# 安装 GDB

sudo apt update
# 通过以下命令安装
sudo apt install build-essential gdb

# 确认是否安装成功
gcc --version
g++ --version
gdb --version
```

## 2. CMake 安装

```bash
# 安装
sudo apt install cmake

# 安装是否成功
cmake --version
```

# GCC 编译器

1. Linux 开发 C/C++ 一定要熟悉 GCC

2. vscode 就是通过调用 GCC 编译器编译 C/C++ 文件

## 编译过程(基本命令 ：g++ Flags target-file prerequisites)

### 1. 预处理  Pre-Processing					// .i 文件

```bash
# -E 选项只是编译器进队输入文件进行预处理
# 进行宏替换 得到 C/C++ 文件
g++ -E -o test.i test.cpp
```

### 2. 编译 - Compiling								// .s 文件

```bash
# -S 编译选项告诉 g++ 在为 C++ 代码产生汇编语言文件后停止编译
# g++ 产生的汇编语言文件的缺省扩展名是 .s
g++ -S test.i -o test.s
```

### 3. 汇编 - Assembling							// .o 文件

```bash
# -C 选项告诉 g++ 仅把源代码编译为机器语言的目标代码
# 缺省时 g++ 建立的目标代码文件有一个 .o 的扩展名
g++ -c test.s -o test.o
```

### 4. 链接 - Linking									// bin 文件

```bash
# -o 编译选项来为将生成的可执行文件用指定的文件名
g++ -o test test.o
```

### 5. 运行

```bash
./test
```

### 6. 可以直接一步到位

```bash
# 编译
g++ test.cpp -o test
# 运行
./test
```

## g++ 重要编译参数

1. -g	编译带调试信息的可执行文件

```bash
# -g 选项告诉 GCC 产生能被 GNU 使用的调试信息，以调试程序
# 不带 -g 选项是调试不了的
# 产生带调试信息的可执行文件 test
g++ -g test.cpp -o test
```

2. -o[n] 优化源代码

```bash
# -o 默认的优化程度 相当于 -o1

# -o0 不优化

# -o1

# -o2 最常用的

# -o3
```

3. -l（链接系统库文件） 和 -L（链接自定义库文件）

```bash
# -l (小写) 紧接着库名
# 会在/lib /usr/lib /usr/local/lib 三个库中找
g++ -lglog test.cpp

# -L (大写) + 完整的文件路径(绝对路径)
g++ -L/home/lucky/myTestLibFolder test.cpp
```

4. -I 指定自定义头文件搜索目录

```bash
# -I
# /usr/include 目录一般是不用指定的，gcc知道去这里找
# 自定义的头文件或者内置 include 文件不在 /usr/include 文件夹中
# 需要自己用 -I 参数指定头文件目录

g++ -I/myIncludePath test.cpp
```

5. -Wall	打印警告信息

```bash
# 打印 gcc 提供的警告信息
g++ -Wall test.cpp
```

6. -w	关闭警告信息

```bash
# 关闭所有警告信息
g++ -w test.cpp
```

7. -std=c++11	设置编译标准

```bash
# 使用 C++11 标准编译
g++ -std=c++11 test.cpp
```

8. -o	指定输出文件名

```bash
# 指定即将产生的文件名
# 指定输出可执行文件名为 test
g++ -o test test.cpp
./test

# 没有 -o test 默认输出 a.out
g++ test.cpp
./a.out
```

9. -D	定义一个宏

```bash
# 常用场景：
# -DDEBUG 定义 DEBUG 宏，这个DEBUG 用于开启和关闭 DEBUG
```

示例代码：

```c++
#include <iostream>
int main() {
    #ifdef DEBUG
    	printf("调试代码\n");
    #endif
    	printf("功能代码\n")
}

g++ -DDEBUG main.cpp
```

## 案例

```bash
静态库.a后缀 和 动态库.so后缀
g++ main.cpp -Iinclude -lswap -Lsrc -o main
./main
```

# 调试器GDB

```bash
gdb									# open gdb debugger
layout next							# open relative main function
file [executable file]				# debug which file
b [function name or line number] 	# set a breakpoint
run									# run file to breakpoint
next or n 							# next line
step or s							# next step, This command will into the function
quit								# end of gdb
```

**print 大法用于调试也很重要**