
### Beyond Compare

> 官网：[beyondcomparepro.com](https://www.beyondcomparepro.com/)


#### 问题记录

##### 1. 十六进制文件比较，自动对齐导致留空问题

1. 点击工具栏`规则`；
2. 在弹出的对话框中，点击`比较`选项卡，对齐选择`无`（默认为`完成`）。

##### 2. Linux系统上，遇到符号链接，对比的是符号链接本身，而不是其指向的文件

1. 菜单栏 `Session` 》`Session Settings`；
2. 在淡出的对话框中，点击`Handling` 》`Follow symbolic links`。

##### 3. 30天试用期过期后无法使用

1. 打开`regedit.exe`；
2. 删除项`HKEY_CURRENT_USER\Software\Scooter Software\Beyond Compare 4`下的二进制值`CacheID`；

```bat
:: 删除CacheID值
reg delete "HKEY_CURRENT_USER\Software\Scooter Software\Beyond Compare 4" /v CacheID

:: 查询CacheID值
reg query "HKEY_CURRENT_USER\Software\Scooter Software\Beyond Compare 4" /v CacheID
```

