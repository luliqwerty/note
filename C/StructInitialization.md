# struct 定义

```c
struct book {
    char* name;
    char* id;
    char* layout;
    int pageNum;
}
```

# 定义时赋值

```c
struct book book1 = {"深入理解计算机系统", "11214777", "机械出版社", 100};
```



# 定义后赋值

```c
struct book book2;
book2.name = "";
book2.id = 111;
book2.layout = "";
book2.pageNum = 100;
```

# C风格乱序赋值

```c
struct book book3 {
    // 未指定成员的默认为结构体定义中的下一个成员
    .layout = "",
    .pageNum = 100,
    .name = "",
    // 下面对应的值是 id - 结构体定义中 name 的下一个
    1000,
}
```

# C++风格乱序赋值

```c++
struct book book4 {
    name: "Effective Java",
    layout: "东北大学出版社",
    id: 10000,
    pagename: 10000,
}
```

## 写在最后

**这些是在看CCC的代码的时候发现的一些以前没有用过的知识点然后在这里记录一下**

