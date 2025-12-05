# 基础语法

## ls （list files）: 列出目录及文件名

-a ：全部的文件，连同隐藏文件( 开头为 . 的文件) 一起列出来

-d ：仅列出目录本身，而不是列出目录内的文件数据

-l ：长数据串列出，包含文件的属性与权限等等数据   —  可用 ll 代替

ls -al ~ ： 列出你「用户家目录」的所有文件 / 目录，并显示详细信息

ls -al ：列出你「当前所在位置」的所有文件 / 目录，并显示详细信息

> 示例： ls -a

**补充：** ls -l / ll 实战补充： 加 -h (Human readable)。它会把文件大小从 4096000 变成 4.0M 或 3.9G。看模型权重文件大小时非常重要

<br>

## cd（change directory）：切换目录

> 示例： cd ~   回到自己的家目录 |  cd..  去到目录上一级

<br>

## pwd（Print Working Directory）：显示目前所在目录

> 示例：pwd

<br>

## mkdir (make directory)：创建新目录

-m : 直接配置，绕过默认权限 (umask) 

-p : 目录递归创建

**补充：**
> mkdir -m 数字权限 目录名称  | 用数字（777、700、755等）指定

> mkdir -m 符号权限 目录名称  |	用符号（如 u=rwx）指定

> 示例：mkdir -p test/test1

无 -p 时会报错

> 示例：mkdir -m 777 test2

<br>

## rmdir（remove directory）：删除目录

> rmdir [-p] 目录名称

参数 p 是指递归删除，类似mkdir

>示例：rmdir -p test/test1

注意： rmdir 仅能删除空的目录， rm 命令删除非空目录

<br>

## cp（copy file）

> cp [参数] 源文件/目录 目标文件/目录 

**注意：** 源文件与目录可以有多个

![cp参数](image\cp参数.png)

<br>

## rm（remove）：移除文件

> rm [-fir] 文件或目录

参数：

-f ：force，忽略不存在的文件，不会出现警告信息

-i ：互动模式，在删除前会询问使用者是否动作

-r ：递归删除


<br>

## mv（move file）：移动文件与目录，或修改名称

> mv [fiu] source1 source2 source3 .... directory

参数：

-f ：若目标文件已经存在，不询问直接覆盖

-i ：已经存在时会询问是否覆盖

-u ：若目标文件存在，且 source 更新，会直接update

**注意：** 修改名称也可以理解为移动文件

