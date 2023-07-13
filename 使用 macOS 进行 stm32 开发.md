# 使用 macOS 进行 stm32 开发

## 〇. 环境

硬件： MacBook Air M2, 2022 年

系统： macOS Sonoma 14.0 Beta

## 一. 安装 CMake

### 1. 安装 brew

在 macOS 中打开终端，系统默认安装了 clang, macOS 中安装需要管理员权限，管理员如果密码为空会失败，先设置下密码

安装 brew

```shell
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install.sh)"
```

### 2. 安装 Command Line Tools for Xcode

进入 https://developer.apple.com/download/all/
搜索 command line tools, 选择最新版本下载.

### 3. 安装编译环境 安装 make 和 clang

```shell
brew install make

brew install clang

brew install clang++
```

### 4. 安装 CMake

进入 https://cmake.org/download/
选择 macOS 对应的 CMake 版本下载.tar.gz(我是 3.27.0 版本)

进入下载目录, 解压并安装 CMake

```shell
tar -xvf cmake-3.27.0.tar.gz

cd cmake-3.27.0

./configure

make -j32
```

### 5. 安装编译好的 cmake

```shell
sudo make install
```

### 6. 查看 cmake 版本

```shell
cmake --version
```

## 二. 安装 Arm GNU Toolchain

### 1. 下载 Toolchain

进入 https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads

下载并运行 arm-gnu-toolchain-12.2.rel1-darwin-arm64-arm-none-eabi.pkg (注意如果不是 Apple Silicon, 请选择适配的版本)

安装完成后进入访达-应用程序可以看到 ArmGNUToolchain 文件夹. 此时工具链还需要添加到系统 PATH 中才能被编译器所访问.

### 2. 配置 PATH

打开终端 输入

```shell
printenv
```

可以看到 PATH 中包含的文件夹. 我们需要将 Toolchain 所在的文件夹(/Applications/ArmGNUToolchain/12.2.rel1/arm-none-eabi/bin)添加进 PATH 中.

终端输入

```shell
vi ~/.zshrc
```

按 A 键进入输入模式, 输入

```shell
export PATH=$PATH:/Applications/ArmGNUToolchain/12.2.rel1/arm-none-eabi/bin
```

按 Esc 退出输入模式, 输入:wq 保存并退出, 此时 Toolchain 路径已被配置进 PATH 中.

新建一个终端窗口, 再次输入 printenv, 可以看到文件夹确实已被添加到 PATH 中.

## 三. 配置 VS Code

VS Code 安装过程从略.

安装完毕后下载插件 Cortex-Debug, CMake Tools.

打开一个 STM32 工程, 进入 CMakeLists.txt 编译 CMake.

编译完成后点击侧边栏的 CMake, 生成.elf 文件.

生成完成后点击侧边栏到运行和调试, 插入 ST-Link 和目标板, 选择 Cortex Debug 并运行, 程序顺利烧写进 MCU 中.

## 四. 参考

1. [cmake使用方法详解 - Windows Linux MacOS cmake安装教程](https://zhuanlan.zhihu.com/p/560253743)
2. [how to install gcc-arm-none-eabi at Mojave MacOS](https://stackoverflow.com/questions/59861085/how-to-install-gcc-arm-none-eabi-at-mojave-macos)
