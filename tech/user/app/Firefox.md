### Firefox Internet Browser

> 官网：[mozilla.org](https://www.mozilla.org/)


#### 问题记录

##### 1. 每次打开Firefox，都会弹出更新提示，设置页面没有关闭更新的选项

> 参考：https://zhuanlan.zhihu.com/p/349453631

*Windows方式一：安装目录创建策略文件*
1. 创建策略文件`<Firefox 安装目录>\distribution\policies.json`，内容如下：

```json
{
    "policies": {
        "DisableAppUpdate": true
    }
}
```

2. 之后，Firefox设置页面`检查更新(C)`按钮变为灰色，提示`更已被系统管理员禁用`。

*Windows方式二：修改注册表*
1. 以管理员身份打开`regedit.exe`；
2. 修改项`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Mozilla\Firefox`下的DWORD值`DisableAppUpdate`为1；
3. 之后，Firefox设置页面`检查更新(C)`按钮变为灰色，提示`更已被系统管理员禁用`。

```bat
:: 添加或修改DisableAppUpdate值为1
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Mozilla\Firefox" /v DisableAppUpdate /t REG_DWORD /d 1

:: 查询DisableAppUpdate值
reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Mozilla\Firefox" /v DisableAppUpdate
```

