### 串口


#### 问题记录

##### 1 更改串口号（例如COM3->COM6）

1. 打开设备管理程序`devmgmt.msc`；
2. 选择要修改的串口，`端口（COM和LPT）` > `XXXX (COM3)`；
3. 右键菜单选择`属性`，弹出对话框中选择`端口设置` > `高级(A)` > `COM端口号`选择COM6 > `确定`；

##### 2 删除使用的串口记录

1. 打开注册表编辑器`regedit.exe`；
2. 删除项`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\COM Name Arbiter`下的二进制值`ComDB`；
3. 重新插入串口；

```bat
reg delete "HKLM\SYSTEM\CurrentControlSet\Control\COM Name Arbiter" /v ComDB
```

