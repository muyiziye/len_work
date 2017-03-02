tags: 
title: boost 对于文件的处理

#### 对于boost库下面列出在OneCli中常用的一些功能
---
##### 常用函数

exists(path);用于判断目录是否存在

is_directory(path);
is_directory(file_status);用于判断是否是路径

is_regular_file(path);
is_regular_file(file_status);用于判断是否是普通文件

initial_path();得到程序运行时的系统当前路径。

current_path();得到系统当前路径

current_path(const Path&p);改变当前路径

bool create_directory(const Path&dp);建立路径

remove(const Path&p, system::error_code &ec=singular);删除文件

remove_all(const Path&p);递归删除p中所有内容，返回删除文件的数量

rename(const Path1&from_p, const Path2&to_p);重命名

copy_file(const Path1&from_fp, const Path2&to_fp); 拷贝文件

create_directories(const Path&p);建立路径



