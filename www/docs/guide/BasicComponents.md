# BasicComponets
# 基本组件设置
## Nginx
Set Nginx Installed by a Prebuilt CentOS/RHEL Package from the OS Repository
```
$ sudo yum install epel-release
```

Update the repository:
```
$ sudo yum update -y
```

Install NGINX Open Source:
```
$ sudo yum install nginx
```

Verify the installation:
```
$ sudo nginx -v
nginx version: nginx/1.6.3
```

Create the user nginx for Nginx running:
```
$ sudo groupadd www 
$ sudo useradd -g www nginx
```

Check the conf is whether right
```
$ nginx -t
```

Start the Nginx
```
$ service nginx start
```

## Docker
### Docker加速
```
$ curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f1361db2.m.daocloud.io
```

### 查找容器内的用户名及密码
```bash
$ docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
```