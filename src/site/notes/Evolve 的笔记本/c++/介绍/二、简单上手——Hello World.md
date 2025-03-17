---
{"dg-publish":true,"permalink":"/Evolve 的笔记本/c++/介绍/二、简单上手——Hello World/","created":"2025-01-18T11:05:37.809+08:00"}
---

写C++程序其实很简单，直接用记事本写好代码，然后用一个编译器做编译运行就可以了；不过这意味这我们得自己保证语法正确，严重影响开发效率。所以实际应用中我们一般都会使用功能更强大的工具，除了提供编译器外，还可以给我们做语法检查和提醒，方便我们调试程序——这就是所谓的“集成开发环境”（IDE）。

这里我们使用ubuntu系统来演示，首先我们需要一个ide来编辑代码，这里我们选择 vscode,安装好软件后就可以写代码了

在 Ubuntu 系统上编写 C++ 程序的基本步骤如下：

### 1. 安装必要的软件

首先，需要确保系统已安装 C++ 编译器，最常见的是 `g++`。可以通过以下命令进行安装：

```bash
sudo apt update
sudo apt install g++
```

### 2. 编写 C++ 程序

在 Ubuntu 中，使用文本编辑器（如 `nano`、`vim`、`gedit` 等）编写 C++ 程序。例如，创建一个简单的 `hello.cpp` 程序：

```cpp
#include <iostream>

void greet(); // 函数声明

int main() {
    greet(); // 调用函数
    return 0;
}

void greet() { // 函数定义
    std::cout << "Hello, World!" << std::endl;
}
```

### 3. 编译和运行程序

使用 `g++` 编译器来编译 C++ 程序。假设文件名为 `hello.cpp`，在终端中运行以下命令：

```bash
g++ hello.cpp -o hello
./hello
```

这将编译 `hello.cpp`，并生成名为 `hello` 的可执行文件，然后运行它。

### 4. 函数链接问题

当多个 C++ 文件（例如 `file1.cpp` 和 `file2.cpp`）中包含不同的函数定义时，编译器需要链接这些文件。链接是将多个目标文件（`.o` 文件）合并为一个可执行文件的过程。C++ 支持将函数的声明放在头文件中，并在其他源文件中定义函数。

假设有两个文件：`file1.cpp` 和 `file2.cpp`。

#### file1.cpp:

```cpp
#include <iostream>

void function_in_file1(); // 函数声明

int main() {
    function_in_file1();
    return 0;
}
```

#### file2.cpp:

```cpp
#include <iostream>

void function_in_file1() { // 函数定义
    std::cout << "Function in file2 is called." << std::endl;
}
```

#### 编译和链接多个文件：

你需要将两个文件编译并链接在一起：

```bash
g++ file1.cpp file2.cpp -o program
./program
```

这样，`g++` 会将 `file1.cpp` 和 `file2.cpp` 编译成目标文件，并链接它们生成最终的可执行文件。

### 5. 处理链接错误

如果有多个函数定义冲突，编译器会报错。例如，两个文件中有相同名字的函数定义，这时链接会失败。为避免这种情况，可以使用 `inline` 关键字或者将函数声明放到不同的命名空间中。

#### 例如：

```cpp
namespace file1 {
    void greet() { std::cout << "Hello from file1." << std::endl; }
}

namespace file2 {
    void greet() { std::cout << "Hello from file2." << std::endl; }
}
```

这种方式可以避免同名函数的冲突。
![Pasted image 20250117231536.png](/img/user/Pasted%20image%2020250117231536.png)
