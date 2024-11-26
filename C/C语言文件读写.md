# C 语言 文件读写

在上一章节中我们学习了 C 语言如何处理标准输入和输出设备。本章我们将介绍 C 程序如何创建、打开、关闭文本文件或二进制文件。

一个文件，无论它是文本文件还是二进制文件，都是代表了一系列的字节。 C 语言不仅提供了访问顶层的函数，也提供了底层（OS）调用来处理存储设备上的文件。

## 打开文件

fopen()函数用来创建一个新的文件或者打开一个已有的文件。

```
FILE *fopen( const char * filename, const char * mode );
```

- 调用 `fopen` 函数会初始化一个 **FILE** 结构的对象。 结构 **FILE** 包含了所有用来控制流的必要的信息
- **filename** 是字符串，用来命名文件
- **mode** 是文件访问模式

### mode

访问模式 **mode** 的值可以是下列值中的一个或多个组合

| mode | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| r    | 打开一个已有的文本文件，允许读取文件                         |
| w    | 打开一个文本文件，允许写入文件。如果文件不存在，则会创建一个新文件 'w' 模式会导致程序会从文件的开头写入内容。 |
| a    | 打开一个文件并以追加模式写入文件。如果文件不存在，则会创建一个新文件 'a' 模式会导致程序会在已有的文件内容中追加内容。 |
| r+   | 打开一个文本文件，允许读写文件。 相当于 `rw` 组合            |
| w+   | 打开一个文本文件，允许读写文件。 如果文件已存在，则会被截断为零长度 如果文件不存在，则会创建一个新文件 |
| a+   | 打开一个文本文件，允许读写文件。 如果文件不存在，则会创建一个新文件。 读取会从文件的开头开始，写入则只能是追加模式。 |

如果处理的是二进制文件，则需使用下面的访问模式来取代上面的访问模式：

```
"rb", "wb", "ab", "rb+", "r+b", "wb+", "w+b", "ab+", "a+b"
```

## 关闭文件

在 C 语言中，文件打开了用完了就要及时关闭。可以使用 fclose()函数来关闭文件。

```
int fclose( FILE *fp );
```

- 如果成功关闭文件， **fclose( )** 函数返回零
- 如果关闭文件时发生错误，函数返回 **EOF**

而 `fclose` 函数的实际操作会清空缓冲区中的数据，关闭文件，并释放用于该文件的所有内存。

EOF 是一个定义在头文件 `stdio.h` 中的常量。


C 标准库提供了各种函数来按字符或者以固定长度字符串的形式读写文件。

## 写入文件

#### 1. fputc()函数是把字符输出到流中的最简单的函数

```
int fputc( int c, FILE *fp );
```

函数 **fputc()** 把参数 c 的字符值写入到 fp 所指向的输出流中。 如果写入成功，它会返回写入的字符，如果发生错误，则会返回 **EOF** 。

#### 2. fputs()函数则可以把一个以 null 结尾的字符串写入到流中

```
int fputs( const char *s, FILE *fp );
```

函数 **fputs()** 把字符串 **s** 写入到 fp 所指向的输出流中。 如果写入成功，它会返回一个非负值，如果发生错误，则会返回 **EOF**

#### 3. fprintf() 函数也可以把一个字符串写入到文件中。

```
**int fprintf(FILE *fp,const char *format, ...)*
```

### 范例

```
/**
 * file: main.c
 * author: 简单教程(www.twle.cn)
 */

#include <stdio.h>

int main()
{
   FILE *fp = NULL;

   fp = fopen("test.txt", "w+");

   //使用 fputc 向文件中写入 H 字符
   fputc('H',fp);

   // 使用 fprintf 向文件中输入 ello 简单教程
   // 注意不要忘记最后的换行符
   fprintf(fp, "ello 简单教程\n");

   // 使用 fputs 向文件中写入 Hello www.twle.cn
   fputs("Hello www.twle.cn\n", fp);

   fclose(fp);

   return 0;
}
```

编译和运行程序，当前目录下会创建名为 `test.txt` 的文件，其内容如下

```
Hello 简单教程
Hello www.twle.cn
```

## 读取文件

#### 1. 使用 fgetc()函数可以从文件中读取单个字符

```
int fgetc( FILE * fp );
```

**fgetc()** 函数从 fp 所指向的输入文件中读取一个字符，返回值是读取的字符。 如果发生错误则返回 **EOF** 。

#### 2. fgets() 函数则可以从流中读取一个字符串

```
char *fgets( char *buf, int n, FILE *fp );
```

函数 **fgets()** 从 fp 所指向的输入流中读取 n - 1 个字符。 它会把读取的字符串复制到缓冲区 **buf** ，并在最后追加一个 **null** 字符来终止字符串。

如果这个函数在读取最后一个字符之前就遇到一个换行符 '\n' 或文件的末尾 EOF，则只会返回读取到的字符，包括换行符。

#### 3. 你也可以使用 fscanf()函数从文件中读取字符串

```
int fscanf(FILE *fp, const char *format, ...)
```

fscanf 函数来从文件中读取字符串，但是在遇到第一个空格字符时，它会停止读取

### 范例

假设和 **main.c** 同一个目录下存在 `test.txt` 文件，内容如下

```
Hello 简单教程
Hello www.twle.cn
```

我们使用 `fscanf` 和 `fgets` 从 `test.txt` 中读取内容

```
/**
 * file: main.c
 * author: 简单教程(www.twle.cn)
 */

#include <stdio.h>

int main()
{
   FILE *fp = NULL;
   char buff[255];
   char c;

   fp = fopen("test.txt", "r");

   c = fgetc(fp);
   printf("the first character of test is:%c\n",c);

   fscanf(fp, "%s", buff);
   printf("1 : %s\n", buff );

   fgets(buff, 255, (FILE*)fp);
   printf("2: %s\n", buff );

   fgets(buff, 255, (FILE*)fp);
   printf("3: %s\n", buff );
   fclose(fp);

}
```

编译和运行上面的代码，输出结果如下

```
the first character of test is:H
1 : ello
2:  简单教程

3: Hello www.twle.cn
```

1. 首先，使用 fgetc 从 `test.txt` 中读取第一个字符，也就是 `H`。
2. 然后，使用 **fscanf()** 方法只读取了 **ello** ，因为它在后边遇到了一个空格。
3. 再次，调用 **fgets()** 读取剩余的部分，直到行尾。
4. 最后，调用 **fgets()** 完整地读取第二行

## 二进制 I/O 函数

下面两个函数用于二进制输入和输出，它们可以用于存储块的读写 - 通常是数组或结构体

- size_t fread(void *ptr, size_t size, size_t nmemb, FILE* stream)

  从给定流 **stream** 读取数据到 **ptr** 所指向的数组中

- size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE* stream)

  把 **ptr** 所指向的数组中的数据写入到给定流 **stream** 中