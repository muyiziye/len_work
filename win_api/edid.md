title: About EDID
tags: 

#### 对edid做个简单的说明。

**1.** 使用OneCli我们会在Hardware_inventory页面下面找到monitor，在其下面有个resolution列表，这个resolution列表与我们直接在桌面右键->屏幕分辨率取得的是不一致的。

**2.** 这个数据是包含在mointor下面的EDID(Extended Display Identification Data)中的,我们可以通过注册表来查看EDID数据，其路径为(HKEY_LOCAL_MACHINE→SYSTEM→CurrentContorlSet→Enum→DISPLAY→<using monitor name\>→Device Parameters→EDID).

**3.** 这里有个文档来简单说明[EDID文档](http://wenku.baidu.com/view/b77ee817482fb4daa58d4b5d.html?from=search)
