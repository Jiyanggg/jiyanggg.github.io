

## 参考

https://dunwu.github.io/linux-tutorial/linux/cli/#%F0%9F%93%96-%E5%86%85%E5%AE%B9

### 1. 解压/压缩

```
tar zxvf file.tar /tmp
tar zcvf file.tar /tmp/file
unzip test.zip 
```

### 2. 后台运行可执行文件

```
nohup python bash.py > /tmp/bash.log 2&>1 &

# log 是保存输出的文件名称；
# 2>&1 表示不仅命令行正常的输出保存到log中，产生错误信息的输 出也保存到log文件中；
# & 表示该进程在后台运行；
# nohup 表示进程在当用户注销（logout）或者网络断开时不会被终止。
```

### 3. 查看特定网络端口的进程 & 杀死

```
netstat -lnp|grep [PORT]
```

```
kill [PID]
```

### 4. 查看磁盘情况并追踪至具体大文件

查看整体情况

```
df -h
```

转到根目录, 逐层查看大文件位置

```
cd /
du -sh *
```

### 5. Centos 开启 NFS 

https://qizhanming.com/blog/2018/08/08/how-to-install-nfs-on-centos-7

### 6. 定时删除文件

```
vim /etc/crontab

 0 0 23  L  *  ? root find /var/log -type f -name "messages-[0-9]*"  | xargs rm -rf
```