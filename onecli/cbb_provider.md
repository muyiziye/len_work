tags: 
title: cbb provider 编译

#### cbb provider 编译

**1.** 环境搭建

 - 从服务器上面下载软件VMware Workstation并安装。
路径为:\\10.240.196.116\Data\SharedFolder\panpeng\VMware-workstation_full_12.1.1.6932.exe

 - 从服务器上面下载VMware Workbench（Virtual Machine)。目前cbbprovider暂时只能在版本5.5上编译, 将其中5.5涉及的4个文件都下载。
路径为：\\10.240.196.116\Data\SharedFolder\wangliang13\Virtual Machines\

 - 创建VMWare ESXi Workbench环境
打开VMware Workstation，open a Virtual Machine，选中VMWare ESXi 5.5中后缀为.vmx的文件，此时已经开启了一个新的虚拟环境。用户名密码:root vmware

**2.** 编译代码

 - 从git上获取最新代码，git@git.icelab.lenovo.com:chensh4/cbbprovider.git

 - 解压代码，将代码pciinfo 拷贝到目录/opt/vmware/cimpdk-5.5.0-1198611/目录下，cd到pciinfo目录下面运行make命令开始编译。

 - 生成的provider文件为：./build/vib/vmware-esx-provider-pciinfo.vib

**3.** 签名

  - 发送出去之前需要给vib文件进行签名，使用命令

  - vibauthor -s -v build/vib/vmware-esx-provider-pciinfo.vib -k /opt/vmware/vibtools/testcerts/accepted.key -r /opt/vmware- /vibtools/testcerts/accepted.cert，

  - 其中只需要将vib文件替换为需要的即可。

**4.** 调试

  - 将文件vmware-esx-provider-pciinfo.vib 上传至目标ESXi的环境

  - 在安装之前将看门狗关闭：/etc/init.d/sfcbd-watchdog stop
  
  - 安装vib：esxcli software vib install -v vmware-esx-provider-pciinfo.vib --maintenance-mode --no-sig-check
  - 检查是否安装成功： esxcli software vib list | grep pciinfo

  - /etc/init.d/sfcbd-watchdog start 

    Notes:
    1) 在安装过程中出现ibm_pciinfo_provider_autorun.sh这个脚本没有运行权限或者格式不对，可以将该文件删除在安装。

**5.** pciinfo工作流程简介

 - lspci 此命令是用来显示系统中所有PCI总线设备或连接到总线上的所有设备的工具。

 - esxcli hardware pci list,该命令是用来列出在此host上面的所有的Pci设备的。具体可以参照文档 [exscli](http://pubs.vmware.com/vsphere-51/index.jsp?topic=%2Fcom.vmware.vcli.ref.doc%2Fesxcli_hardware.html)

**6.** 在编译中可能会出现的问题，编译之前需要先修改下文件，oss/sfcb/src/cmpift.h中需要将669行的函数注释掉。

**7.** 编译完成之后，可以直接替换掉.so文件即可，路径为/build/stage/usr/lib/cim/libpciinfoprovider.so,然后重启下sfcb服务即可

---