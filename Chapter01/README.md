## 第一章 开始

### 1. 编写简单的C++程序

每个C++程序都包含一个活多个函数（function），其中一个必须命名为 `main` 。

操作系统通过调用main来运行C++程序。

```c++
int main()
{
  return 0;
}
```

> main函数的返回类型必须为int，即整数类型。
>
> `int类型`是一种 `内置类型（build-in type）`，即语言自身定义的类型。

**函数定义包含的四部分**

> - 返回类型（return type）
> - 函数名（function name）
> - 参数列表（parameter list）：允许为空。
> - 函数体（function body）
>   - 以花括号组成的语句块（block of statement）。
>   - return：
>     - 结束函数的执行。
>     - 向调用者返回一个值。（返回值类型与函数的返回类型相同）
>     - ⚠️注意点：return 语句末尾以`分号`结束。

⚠️注意：*大多数C++语句都以 `分号` 表示结束*。

 在大多数OS中，在main函数的返回值中被用来指示状态，***返回值0表示成功，非0返回值的含义由系统定义***。主要是来**指出错误类型**。

### 2. 编译、运行程序

基本上PC机上的编译器都具有集成开发环境（Integrated Development Environment，IDE）：将编译器与其他程序创建和分析工具封装在一起。

#### 2.1 程序源文件命名约定

程序文件通常称为源文件（source file）。

大多数系统中，源文件的名字以一个后缀作为结尾。**后缀的作用**：告知系统某文件是C++程序。

常见的后缀：**`.cc、.cxx、.cpp、.cp及.c`**。

#### 2.2 了解编译器gcc（g++）

*gcc命令可以将源文件编译成可执行文件*。

- 执行文件
  - Windows：可执行文件名是以 `.exe` 结尾。一般情况下，忽略其扩展名 `.exe`。
  - Linux：可执行文件以 `.out` 结尾。
- **查看gcc编译器版本**

```shell
[root@centos8 ~]# gcc --version
gcc (GCC) 8.3.1 20191121 (Red Hat 8.3.1-5)
Copyright (C) 2018 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

- **gcc使用手册**

```shell
[root@centos8 ~]# gcc --help
Usage: gcc [options] file...
Options:
  -pass-exit-codes         Exit with highest error code from a phase.
  --help                   Display this information.
  --target-help            Display target specific command line options.
  --help={common|optimizers|params|target|warnings|[^]{joined|separate|undocumented}}[,...].
                           Display specific types of command line options.
  (Use '-v --help' to display command line options of sub-processes).
  --version                Display compiler version information.
  -dumpspecs               Display all of the built in spec strings.
  -dumpversion             Display the version of the compiler.
  -dumpmachine             Display the compiler's target processor.
  -print-search-dirs       Display the directories in the compiler's search path.
  -print-libgcc-file-name  Display the name of the compiler's companion library.
  -print-file-name=<lib>   Display the full path to library <lib>.
  -print-prog-name=<prog>  Display the full path to compiler component <prog>.
  -print-multiarch         Display the target's normalized GNU triplet, used as
                           a component in the library path.
  -print-multi-directory   Display the root directory for versions of libgcc.
  -print-multi-lib         Display the mapping between command line options and
                           multiple library search directories.
  -print-multi-os-directory Display the relative path to OS libraries.
  -print-sysroot           Display the target libraries directory.
  -print-sysroot-headers-suffix Display the sysroot suffix used to find headers.
  -Wa,<options>            Pass comma-separated <options> on to the assembler.
  -Wp,<options>            Pass comma-separated <options> on to the preprocessor.
  -Wl,<options>            Pass comma-separated <options> on to the linker.
  -Xassembler <arg>        Pass <arg> on to the assembler.
  -Xpreprocessor <arg>     Pass <arg> on to the preprocessor.
  -Xlinker <arg>           Pass <arg> on to the linker.
  -save-temps              Do not delete intermediate files.
  -save-temps=<arg>        Do not delete intermediate files.
  -no-canonical-prefixes   Do not canonicalize paths when building relative
                           prefixes to other gcc components.
  -pipe                    Use pipes rather than intermediate files.
  -time                    Time the execution of each subprocess.
  -specs=<file>            Override built-in specs with the contents of <file>.
  -std=<standard>          Assume that the input sources are for <standard>.
  --sysroot=<directory>    Use <directory> as the root directory for headers
                           and libraries.
  -B <directory>           Add <directory> to the compiler's search paths.
  -v                       Display the programs invoked by the compiler.
  -###                     Like -v but options quoted and commands not executed.
  -E                       Preprocess only; do not compile, assemble or link.
  -S                       Compile only; do not assemble or link.
  -c                       Compile and assemble, but do not link.
  -o <file>                Place the output into <file>.
  -pie                     Create a dynamically linked position independent
                           executable.
  -shared                  Create a shared library.
  -x <language>            Specify the language of the following input files.
                           Permissible languages include: c c++ assembler none
                           'none' means revert to the default behavior of
                           guessing the language based on the file's extension.

Options starting with -g, -f, -m, -O, -W, or --param are automatically
 passed on to the various sub-processes invoked by gcc.  In order to pass
 other options on to these processes the -W<letter> options must be used.

For bug reporting instructions, please see:
<http://bugzilla.redhat.com/bugzilla>.
```

- 程序状态的获取

> Windows：`echo %ERRORLEVEL%`
>
> Uniux/Linux：`echo $?`

➡️更多编译内容知识点，请等待***《编译原理》***和 ***《高级编译器设计与实现》*** 书籍笔记以及 ***CS151课程*** 笔记等内容的更新。

### 3. 初识输入输出(IO)

C++使用标准库（standard library）来提供IO机制。

**`iostream库`**包含：**`istream（输入流）`** 和 **`ostream（输出流）`**。一个流表示一个字符序列。

#### 3.1 标准IO对象

- **`istream（输入流）`**类型的对象为 **`cin`**，也叫做标准输入（standard input）。
- **`ostream（输出流）`**类型的对象为 **`cout`**，也称为标准输出（standard output）。

其他两个**`ostream（输出流）`**对象

- **cerr**：输出警告和错误消息。
- **clog**：输出程序运行时的一般性信息。

#### 3.1 IO库的程序例子

```C++
#include<iosteam>
int main()
{
  std::cout<< "Enter two numbers:"<<std::endl;
  int v1 = 0,v2 = 0;
  std::cin >> v1 >> v2;
  std::cout<< "The sum of "<< v1 << " and " << v2
    			 << " is " << v1 + v2 << std::endl;
  return 0;
}
```

`#include<>` 指令都放在源文件的开始位置。出现在所有函数之外。

一般在 **`尖括号<>` ** 中包含头文件***（header）***。告诉编译器想要使用的库名。

***头文件（header）***：类的类型一般情况下存储在头文件中。**系统自带** 的标准库头文件使用 **`尖括号<>` **, **用户自定义** 的非标准库的头文件使用 **`双引号""`** 。

**头文件声明** 写在 `.h` 文件中，**函数的定义实现** 等写在 `.cpp` 文件中。

`endl` :操纵符（manipulator）的特殊值。**作用**：结束当前行，并将与设备关联的缓冲区（buffer）中内容刷到设备中。

⚠️注意：对于 `>>` 和 `<<` 返回的结果都是左操作数，也就是输入流和输出流其本身。

#### 3.2 文件结束符

Windows系统：`Ctrl + Z`

Unix / Linux / Mac OS系统：`Ctrl + D`

### 4. 注释

作用：帮助读者理解程序（增强代码的可读性）。

用途：一般概述算法，确定变量用途，解释难懂的代码段。

✅编译器会忽略注释。对程序不会产生影响。

两种注释方式：

✅1⃣️单行注释：`//`

✅2⃣️多行注释：`/* */`。编译器会自动忽略 `/*` 和 `*/` 之间的内容都作为注释内容忽略。⚠️注意：***注释不能嵌套***。

### 5. 控制流

#### 5.1 while语句

语法格式：

```C++
while(condition)
  statement
```

程序循环执行，直到交替检测 `condition为假` 时停止。

条件(condition)：一个产生真或假的结果的表达式。

#### 5.2 for语句

语法格式：

```c++
for(init_statement,condition,expression)
  statement
```

每个for语句都包含两部分：**`循环头`** 和 **`循环体`**。循环头控制循环体的执行次数，由三部分组成：

- *一个初始化语句（init_statement）*
- *循环条件（condition）*
- *表达式（expression）*

#### 5.3 if语句

语法格式

```c++
if(condition)
	statement01
else
	statement02
```

判断条件 `condition为真` 时，直接执行statement01，否则执行statement02。

⚠️注意：C++中 用 `=` 进行赋值，用 `==` 作为相等运算符。切忌混用。

👉Tips

- C++程序格式自由，不在乎缩进、注释以及换行符，通常不会影响程序的语义。
- 左花括号必须是main的形参列表后第一个非空、非注释的字符。

### 6. 类概述

一个 **类（class）** 定义了一个 *类型名* 及其 *关联的一组操作*。

一般情况下，类的作者决定了类类型对象上可以使用的所有操作。

#### 6.1 成员函数（类方法）

使用 `点运算符(.)` 调用。例：

```C++
item1.isbn() == item2.isbn()
```

调用名为 isbn 的 成员函数（member function）。

成员函数是定义类的一部分的函数，有时叫作方法（method）。

通常一般以一个类对象的名义来调用成员函数。例：

```C++
item1.isbn()
```

调用运算符是一对圆括号，里面放置实参（argument）列表（可能为空）。
