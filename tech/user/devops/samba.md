
### Samba Service

> 官网：
> - [samba.org](https://www.samba.org)

#### 安装使用

##### 服务端启动服务

```sh
# 查看服务启动状态
systemctl status  smbd

# 启动/停止/重启服务
sudo systemctl start smbd
sudo systemctl stop  smbd
sudo systemctl restart smbd
```

#### 服务端配置

Samba服务端配置文件
```sh
sudo vim /etc/samba/smb.conf
```

##### 只读共享

```ini
[shr_ro]
  comment = Samba Read-Only Share
  path = /srv/smb/ro
  browseable = yes
  writeable  = no
```

##### 可读可写共享

```ini
[shr_rw]
  comment = Samba Read-Write Share
  path = /srv/smb/rw
  browseable = yes
  writeable  = yes
```

##### 用户个人目录

每个用户看到的内容实际对应不同的目录。

```ini
[usr]
  comment = Samba Personal Directory
  path = /srv/smb/usr/%U
  browseable = yes
  writeable  = yes
  valid users = ian tst
```

##### 同组用户公共目录

同组用户都可读可写，任何用户创建的目录或文件，同组其他用户均可读可写。

```ini
[pub]
  comment = Samba Public Directory
  path = /srv/pub
  browseable = yes
  writeable  = yes
  force group = fisheep
  force create mode = 0666
  force directory mode = 0777
```

##### 所有用户以某个用户身份访问

```ini
[common]
  comment = Samba Common Direcotry
  path = /srv/smb/common
  browseable = yes
  writeable  = yes
  force user = ian
```

##### 新建文件和目录权限继承父目录

正常情况下，
- 新建文件权限由create mask, force create mode决定；
- 新建目录权限由directory mask, force directory mode决定；

inherit permissions覆盖该规则，使用父目录的权限来设置新文件/目录的权限，
- 新建文件继承父目录的read/write权限；
- 新建目录继承父目录的read/write/execute权限，以及setgid；

```ini
[tst]
  comment = Samba Test
  path = /srv/smb/test
  browseable = yes
  writeable  = yes
  inherit permissions = yes
```

#### 问题记录

##### 1 手机/电视盒子等连接不成功

手机/电视盒子可能只支持samba v1.0版本协议，修改服务端支持的最新协议版本。

```sh
sudo vim /etc/samba/smb.conf

[global]
  server min protocol = NT1
```

##### 2 设置必须登录后才可见共享列表

```sh
sudo vim /etc/samba/smb.conf

[global]
  security = user
```

##### 3 特定用户才能看到某些共享列表

```sh
sudo vim /etc/samba/smb.conf

[global]
  config file = /etc/samba/cfg.%U.smb.conf


# cfg.%U.smb.conf中再包含公共的共享目录
sudo vim /etc/samba/cfg.%U.smb.conf

[global]
  include = /etc/samba/inc.common.smb.conf
```

##### 4 隐藏lost+found目录

```sh
sudo vim /etc/samba/smb.conf

[global]
  veto files = /lost+found/
```


