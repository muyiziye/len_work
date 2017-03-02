### 磁盘修复

---

cmd>>diskpart

list disk                 //显示磁盘编号

select disk NO     //选择U盘对应的编号

clean                    //清除分区信息

create partition primary //创建主分区

active                    //激活

format fs=ntfs quick //快速格式化

assign                    //分配盘符

exit                         //退出

---