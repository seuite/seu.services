# Useful Linux Command Manual

For System Information checking:
```
$ sudo cat /proc/cpuinfo
```

获取硬件DMI信息
```
$ sudo dmidecode
```

查看端口占用情况
```
netstat -anp | grep '$port'
```
```
lsof -i:'$port'
```
```
ps -aux | grep '$port&process'
```

查看目录/文件占用大小
```
du -sh #查看当前目录总共占用容量
du -lh --max-depth=1 #查看当前目录递归一级子文件和子目录占用的磁盘容量
du -skh '$filename' #查看指定文件大小
```

## 网易云音乐外链链接
    http://music.163.com/song/media/outer/url?id=ID数字.mp3