### 安装windows机器

**1.** 更新固件

  - 更新IMM, 需要根据 [ddlist](http://gsax-pro.labs.lenovo.com/rtpgsa/projects/d/ddlistrepository/index.html) 
来判断需要下载那个版本， 然后根据其去oss上面搜索对应的版本，通过web来更新。或者在imm web网页上看原来的版本，然后找最新的来安装。

  - 更新IMM的方式有三种：
    
    > a. 使用web端来更新。

    > b. 使用OneCli来更新，命令如下 OneCli.exe update flash --imm USERID:PASSW0RD@10.240.198.38 --sftp root:SYS2009health@10.240.197.107/home/liuyang/tmp/ --scope individual --includeid lnvgy_fw_uefi_tee103n-1.00_anyos_32-64 --forceid all --dir E:\fw\Electron --output getIMMMTout --log 5

    > c. 找专门的刷的工具，目前我没有用过。

  - 更新UEFI, 跟IMM一样。但是需要注意的是在刷UEFI的时候，不要让机器处于uefi状态，要么关掉os，要么是在os里面。

  - 这里要强调一下uefi也有第三种方法，需要将uefi芯片取下刷，需要向别的team借工具。

**2.** 安装windows

  - 需要下载windows的iso包，可以从 \\10.240.196.116\Windows OS\Win2016 上面找，key在后面的文件中，然后使用工具做成U盘启动盘，注意不要使用preview版本的，因为preview的版本会在一段时间后过期，然后系统就会不时重启，最终不能使用。

**3.** 

  - 需要下载linux的iso包，可以从 \\10.240.196.116\Linux OS 上面找，使用工具做成U盘启动盘。

