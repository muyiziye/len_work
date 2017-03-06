### strtok()

头文件：#include<string.h>

定义：char *strtok(char *s, const char *delim);

说明：strtok()用来将字符串分割成一个个片段，参数s指向分隔的字符串，参数delim则为分隔字符串，当strtok（）在参数s的字符串中发现到参数delim的分割字符时则会将该字符改为\0字符。在第一次调用的时候，strtok（）必须给予参数s字符串，往后的调用则将参数s设置为NULL，每次调用成功则返回下一个分割后的字符串指针。

返回值：返回下一个分割后的字符串指针，如果已经无法分割则返回NULL。

