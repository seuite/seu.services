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
### Docker安装
```
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

### Docker加速
这里使用了我在阿里云上注册的docker加速器
```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v8thd0yh.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 查找容器内的用户名及密码
```bash
$ docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
```