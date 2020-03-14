---
layout:     post                    # 使用的布局（不需要改）
title:      Windows10 子系统安装 Quantum Espresso              # 标题 
subtitle:   安装教程          #副标题
date:       2020-03-12             # 时间
author:     Shang                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    -  教程
---
## 并行环境的安装

### 下载 openmpi

1. 打开[官网]( https://www.open-mpi.org/software/ompi/v4.0/ )，下载需要的版本。

![image-20191119143744757](/img/2020-03-12/image-20191119143744757.png)

2. 打开子系统界面，将下载好的文件复制到你想要安装的文件夹下。这里我安装在了自己的家目录下 ~/。解压。

   ```shell
   tar -zxvf openmpi-4.0.2.tar.gz
   cd openmpi-4.0.2
   vi INSTALL
   ```

   查看安装方式。

   ![image-20191119155407981](/img/2020-03-12/image-20191119155407981.png)

3. 按照上述图片运行，安装即可。在这里，`../configure`可能会报错，仔细阅读报错信息。我遇到的是没有安装g++等编译c++的软件，`sudo apt install` 安装即可。最后一步，可能会提示权限不够，用sudo即可。

4. mpirun: error while loading shared libraries: libopen-rte.so.40: cannot open shared object file: No such file or directory。安装好之后运行的时候，可能会有这样的错误。使用`sudo ldconfig`更新一下即可。

## 安装QE

在安装QE的时候，会自动检测前面安装的并行软件。

1. QE官网下载软件包，解压，进入目录。

2. 确保自己的系统上有 `gcc`, `gfortran`, `make`等编译C语言和Fortran语言的软件。没有的话，自行`sudo apt install ***` 安装。

   ``` shell
   ./configure
   make all
   ```

   两步即可，安装成功。不过编译需要一些时间，耐心等待即可。不想安装QE的全部模块，也可以分开安装。

3. 安装成功后，可以进入PW，PHonon等文件夹的examples目录，运行`./run_all_examples`进行测试。
