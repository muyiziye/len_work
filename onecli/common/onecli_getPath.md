tags: 
title: Different Paths in OneCli

#### 在OneCli中取得路径的方法。

* 1. 在OneCliDirectory.cpp文件中，可以找到下面一些取得对应path的方法。

> string GetExePath(const string &fileName);其返回的是OneCli所在的目录的路径。

> string GetFullPath(const string &inputDir);根据工作目录和传入的路径，返回传入参数路径的绝对路径。

> string getOutputDir();该函数返回的是output路径，也即为--output 后面所带路径的绝对路径。

* 2. 在ArgParser.cpp文件中，取得路径的方法。

> string GetFullpathCommand(),该函数返回的是m_argv[0],在我们实际使用的时候需要自己转换，没有使用OneCliDirectory.cpp中的函数来的方便。

* 3. 使用boost里面的取得路径的方法。（可以搜索下面文章“boost 对于文件的处理”）

> current_path();得到系统当前路径