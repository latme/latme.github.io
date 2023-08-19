
### Windows 11

> 官网：[microsoft.com](https://www.microsoft.com/zh-cn/software-download/windows11)

#### 问题记录

##### 1. 提示设备硬件不满足Win11最低要求

1. 按`Shift + F10`打开命令提示窗口；
2. 执行`regedit`打开注册表编辑器（或执行下述命令）修改注册表；
3. 修改项`HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig`下的DWORD值`BypassTPMCheck`为1，跳过TPM 2.0检查；
4. 修改项`HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig`下的DWORD值`BypassSecureBootCheck`为1，跳过安全检查：

```bat
reg add HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig /v BypassTPMCheck /d 1
reg add HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig /v BypassSecureBootCheck /d 1
```
##### 2. 提示必须登录微软账户，否则不能继续安装

1. 安装前拔掉网线；

##### 3. 提示没有网络，下一步按钮是灰色的；

1. 按`Shift + F10`打开命令提示窗口；
2. 执行`OOBE\BYPASSNRO`；
3. 系统将自动重启，重启后该步骤将多一个按钮`我没有Internet连接`，点击该按钮继续。

