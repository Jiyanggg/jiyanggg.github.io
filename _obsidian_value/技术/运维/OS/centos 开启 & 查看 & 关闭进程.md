### 开启

```
nohup python manage.py > /data/zyj/xadstat/xadstat.log  2&>1 &

其中log是保存输出的文件名称；
2>&1 表示不仅命令行正常的输出保存到log中，产生错误信息的输出也保存到log文件中；
& 表示该进程在后台运行；
nohup表示进程在当用户注销（logout）或者网络断开时不会被终止。
```

### 查看

```
netstat -lnp|grep [PORT]

ps [PID]
```

### 关闭

```
kill -9 [PID]
```

参考：

https://www.cnblogs.com/coder-lzh/p/8977232.html