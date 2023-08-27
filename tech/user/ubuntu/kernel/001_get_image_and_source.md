
### Ubuntu Kernel

> 官网：
> - [releases.ubuntu.com](http://releases.ubuntu.com/)
> - [launchpad.net/ubuntu](https://launchpad.net/ubuntu)
> - [kernel.ubuntu.com/git/ubuntu-stable](https://kernel.ubuntu.com/git/ubuntu-stable)


#### 问题记录

##### 1 下载系统镜像

1. 打开下载网页：`http://releases.ubuntu.com`；
2. 选择要下载的版本，例如 22.04.3 LTS；
3. 选择要下载的文件，包括：
   - 桌面版/服务器版；
   - \*.iso: 安装镜像
   - \*.list: 安装镜像内的文件列表
   - \*.manifest: 安装镜像内的软件包的版本

##### 2 下载镜像对应的源码

> 参考：
> - https://cloud.tencent.com/developer/article/1439068
> - https://wiki.ubuntu.com/Kernel/Dev/KernelGitGuide

   ```sh
   # 查看当前运行系统的精确版本号；
   cat /proc/version_signature

   # 22.04 <--> jammy
   # https://git.launchpad.net/~ubuntu-kernel/ubuntu/+source/linux/+git/jammy/refs/tags
   # https://kernel.ubuntu.com/git/ubuntu-stable/ubuntu-stable-jammy.git
   ```

