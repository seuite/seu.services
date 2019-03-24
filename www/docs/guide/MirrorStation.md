# SEUITE镜像站
由于学校官方镜像站常年处于欠维护状态，故我们单独维护了这样一个非官方镜像站。现已支持CentOS，Ubuntu和EPEL源的rsync和http(s)

# 搭建步骤
## 1. 硬件环境
服务器硬件参数如下：
> CPU: 32 核心 3.0GHz
>
> 内存: 16 GB
>  
> 硬盘: 6 TB (3TBx2 LVM)
>
> 网络: 百兆对等带宽

本镜像站所用容量为
- CentOS 154.38G
- EPEL 232.33G
- Ubuntu 1.30T
- Pypi 

## 2. 同步源
从官方源中选择支持rsync的国内镜像源同步

Ubuntu 源列表：https://launchpad.net/ubuntu/+archivemirrors
```
rsync://mirrors.shuosc.org/ubuntu/
rsync://mirrors.sohu.com/ubuntu/
rsync://mirrors.tuna.tsinghua.edu.cn/ubuntu/
rsync://mirrors.ustc.edu.cn/ubuntu/
rsync://mirrors.yun-idc.com/ubuntu/
```

CentOS 源列表：https://www.centos.org/download/mirrors/
```
rsync://mirrors.tuna.tsinghua.edu.cn/centos/
rsync://mirror.es.its.nyu.edu/centos/
rsync://centos.sonn.com/CentOS/
```

EPEL 源列表：https://admin.fedoraproject.org/mirrormanager/mirrors/EPEL
```
rsync://mirrors.yun-idc.com/epel
rsync://rsync.mirrors.ustc.edu.cn/epel
```

## 3. 同步架构
使用rsync做增量同步，实际使用Tuna的开源项目tunasync的预编译版本v0.3.3

## 4. 系统配置
创建用户及用户组
```bash
groupadd -g 2001 mirrorgroup
useradd -u 2101 -g mirrorgroup mirrors
passwd mirrors
```

切换到mirrors用户
```bash
su mirrors
```

建立应用及数据目录
```bash
mkdir /home/mirrors/tunasync
mkdir /home/mirrors/tunasync/conf
mkdir /home/mirrors/tunasync/db
```

建立镜像数据目录
```bash
sudo mkdir /mirrors
```

修改数据目录用户
```bash
sudo chown -R mirrors:mirrorgroup /mirrors
```

## 同步配置文件
tunasync分为同步服务端和同步客户端，本镜像站为便于管理，均统一放置在`/home/mirrors/tunasync/conf/`目录下

### manager配置(manager.conf)
```
debug = false

[server]
addr = "127.0.0.1"
port = 14242
ssl_cert = ""
ssl_key = ""

[files]
db_type = "bolt"
db_file = "/home/mirrors/tunasync/db/manager.db"
ca_cert = ""
```
- port：监听端口，同客户端同步（在预编译版本中需固定配置为14242）
- ssl设置：在localhost中可不用配置，若需要配置分布式服务器建议配置
- db_file：数据库文件，统一置于`/home/mirrors/tunasync/db/`目录

### worker配置(worker-'$workername'.conf)
```
[global]
name = "centos_worker"
log_dir = "/mirrors/log/tunasync/{{.Name}}"
mirror_dir = "/mirrors"
concurrent = 10
interval = 1440

[manager]
api_base = "http://localhost:14242"
token = "some_token"
ca_cert = ""

[cgroup]
enable = false
base_path = "/sys/fs/cgroup"
group = "tunasync"

[server]
hostname = "localhost"
listen_addr = "127.0.0.1"
listen_port = 16010
ssl_cert = ""
ssl_key = ""

[[mirrors]]
name = "centos"
provider = "rsync"
upstream = "rsync://mirrors.tuna.tsinghua.edu.cn/centos/"
use_ipv6 = false
```
- [global]
    - name: worker 进程名称，用于程序识别
    - log_dir：本进程的tunasync日志路径
    - 




./tunasync manager --config /home/mirrors/tunasync/conf/manager.conf >> /mirrors/log/mirrorlog/manager.log &

tunasync worker --config /home/mirrors/tunasync/conf/worker-centos.conf >> /mirrors/log/plog/worker-centos.log &

tunasync worker --config /home/mirrors/tunasync/conf/worker-epel.conf >> /mirrors/log/plog/worker-epel.log &

tunasync worker --config /home/mirrors/tunasync/conf/worker-pypi.conf >> /mirrors/log/plog/worker-pypi.log &

tunasync worker --config /home/mirrors/tunasync/conf/worker-ubuntu.conf >> /mirrors/log/plog/worker-ubuntu.log &