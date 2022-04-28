### 查看内存状态
```

```
### 查看端口占用情况并删除
```
netstat -anp|grep 80 
```

### 清除内存缓存
```
```

### 查看文件状态
```
```

### 修改 DNS
```
/etc/resolvconf/resolv.conf.d/base（这个文件默认是空的）

在里面插入：
nameserver 8.8.8.8
nameserver 8.8.4.4

如果有多个DNS就一行一个

修改好保存，然后执行

resolvconf -u

再看/etc/resolv.conf，最下面就多了2行
```

### echo
```
echo helloworld > hello.txt
```
