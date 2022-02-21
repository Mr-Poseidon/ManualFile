# cmake随笔

[TOC]

## 博客笔记

1. cmake_minimum_required(VERSION 2.8)	最低版本号要求

2. project(XXX) 项目名称为XXX

3. add_executable(XXX main.cc AAA.cc BBB.cc) 指定生成XXX项目

4. 在含有CMakeLists.txt的目录执行 cmake 命令得到 Makefile 文件

5. 在含有Makefile文件的目录执行 make 命令，编译得到可执行文件

6. aux_source_directory(\<dir\>  \<variable\>) 命令：

   ​		查找指定目录下所有的源文件，并将结果存在指定变量名中。

   ​		例：aux_source_directory(. DIR_SRCS) 将当前目录的所有源文件都存放在DIR_SRCS变量中。

   ​		通过${\<variable\>}的形式对变量名进行引用。

   ​		例：add_executable(XXX ${DIR_SRCS})

7. add_subdirectory(\<dir\>)     添加子目录dir，使得子目录中的CMakeLists.txt 文件和源代码也会被处理。

8. target_link_libraries(XXX AAA)        为项目XXX添加链接库AAA

9. add_library(XXX AAA BBB)   将源代码AAA BBB等编译成静态链接库 XXX

10. configure_file(

    "${PROJECT_SOURCE_DIR}/config.h.in"

    "${PROJECT_BINARY_DIR}/config.h"

    )   ---  加入配置头文件，用于处理CMake对源码的设置

11.  



## Cmake 实践笔记

### 第一章、简介

1. cmake工具链：cmake + make
2. 使用 cmake语言和语法编写CMakeLists.txt文档（每个目录一个）

### 第二章、安装

1. 下载官网：[Download | CMake](https://cmake.org/download/)

### 第三章、第一个Cmake项目

1. PROJECT指令： PROJECT(projectname [CXX] [C] [Java])

2. 建议：直接使用PROJECT_BINARY_DIR和PROJECT_SOURCE_DIR

3. SET指令： SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]])

4. MESSAGE指令： MESSAGE([SEND_ERROR | STATUS | FATAL_ERROR] "message to display" ...)

   SEND_ERROR，产生错误，生成过程被跳过。

   STATUS，输出前缀为—的信息。

   FATAL_ERROR，立即终止所有 cmake 过程。

5. 通过${}来引用变量，IF语句中直接使用变量名

6. 基本语法规则：指令(参数 1 参数 2...) 参数使用中括号括起来，参数之间使用空格或分号隔开

7. 指令大小写无关，参数大小写相关，建议指令全部大写

8. 工程名和生成的可执行文件没有任何关系

9. 双引号""可处理特殊文件名，例如文件名中带有空格字符

10. 文件名不要省略后缀

11. 使用make clean命令对构建结果进行清理

12. 只使用外部构建，方便管理整个项目结构。

    外部构建对原有的工程不会产生任何影响，所有动作都发生在编译目录。

13. 使用外部编译时：

    PROJECT_SOURCE_DIR 指代 工程路径

    PROJECT_BINARY_DIR  指代 编译路径

### 第四章、更好一点的Cmake项目

1. ADD_SUBDIRECTORY 指令： ADD_SUBDIRECTORY(source_dir [binary_dir] [EXCLUDE_FROM_ALL])
2. 可以通过 SET指令 来重新定义**宏变量**
3. 注：在哪里添加库和可执行文件，就在哪里设置库和可执行文件的输出目录
4. 安装编写：参考原书P15-20



