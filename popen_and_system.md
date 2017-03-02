tags: 
title: popen 和 system 的使用

## popen & system

* 相同点: Popen 和 system 都可以执行外部命令

* 不同点: 

> **1.** popen 总是和 pclose一起出现使用的。popen创建一个管道，通过fork来创建一个子进程，然后执行command。其返回值在标准io流中，由于是在管道中，因此数据是单向的，command只能产生输出stdout或者是输入stdin, 所以type的值只能是两个,'w' 或者'r'.r表示command从管道中读取数据，而w表示command表示stdout输出到管道中。command不可以同时读取和输出，popen返回改FIFO数据流的指针。

> **2.** system()函数调用/bin/sh来执行参数指定的命令，/bin/sh 一般是一个软连接，指向某个具体的shell，比如bash，-C选项是告诉shell从字符串command中读取命令。在该command执行期间，SIGCHLD是被阻塞的。在该command命令执行期间，SIGINT和SIGQUIT是被忽略掉的，在收到这两个信号之后没有任何动作。关于system的返回值问题，需要对system的执行过程来说明下，system有三个步骤：a.fork一个子进程, b.在子进程中调用exec函数去执行command;c.在父进程中调用wait去等待子进程结束。如果fork失败，则system函数会返回-1.如果exec执行成功，则返回command通过exit或者是return返回的值。（注意，command顺利执行不代表执行成功，比如command："rm debuglog.txt"，不管文件存不存在该command都顺利执行了）如果exec执行失败，也即command没有顺利执行，比如被信号中断，或者command命令根本不存在，system()函数返回127.
如果command为NULL，则system()函数返回非0值，一般为1.

> **3.** system函数是C89，C99和POSIX.1-2001标准中定义的，是可以跨平台使用的。popen则是在Posix标准函数。

> **4.** 使用system的时候可能会出现一个问题，如果在子进程运行的时候，将信号设置成了SIG_IGN,此时子进程的状态信息会自动回收，而父进程的waitpid就无法捕捉到子进程的状态信息了，而随后调用的wait会阻塞所有的子进程结束，并且返回ECHILD错误，即为没有子进程等待。所以最好不要使用system而是使用popen来解决你的问题。

***

* 使用方法

> **1.** 对于system，头文件为#include <stdlib.h\>,调用方法 int system(const char *command);

> **2.** 对于popen，头文件为#include <stdio.h\>,调用方法 FILE \*popen(const char \*command, const char \*type); int pclose(FILE \*stream);type 有两种'w'和'r'