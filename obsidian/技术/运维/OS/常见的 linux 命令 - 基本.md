
### 参考

https://www.runoob.com/w3cnote/linux-common-command-2.html

https://gywbd.github.io/posts/2014/8/50-linux-commands.html


### 常见目录



```
ls 
```

```
cd ~ 
cd - 
cd /
```

```
pwd
```

```
mkdir
```

```
rm -i *.log
rm -rf /tmp
```

```
mv
```

```
cp
```

```
touch
cat
more 
less
head
tail
```

```
which # 一般用于查找命令/可执行文件所在的路径
whereis # 二进制文件、源文件和帮助手册文件路径的查找
locate # 超快速查找任意文件
find # 直接搜索整个文件目录

find . -regex .*log -size +100k -type f -exec rm -f {} \;
```

```
chmod

# r ：读权限，用数字4表示
# w ：写权限，用数字2表示
# x ：执行权限，用数字1表示
# - ：删除权限，用数字0表示
# s ：特殊权限
```



```
# z: gzip
# c: create
# v: verbose
# f: file
# x: extract

tar -zcvf filename.tar.gz /folder  # 打包压缩 
tar -xvf filename.tar            # 解压
```





```
ln
```

```
grep 
grep -i "the" filename
```

```
ssh user@ip
```

```
sed

sed 's/book/books/' file
```

```
export

export ORACLE_HOME=/u01/app/oracle/product/10.2.0
```


```
mount

mount /dev/sdb1 /u01
```

```
wget 

wget -O taglist.zip http://www.vim.org/scripts/download_script.php?src_id=7701
```

```
crontab

*/10 * * * * /home/ramesh/check-disk-space
```

```
wc

wc(word count)功能为统计指定的文件中字节数、字数、行数，并将统计结果输出
```


```
kill
```


```
ps -A | grep sh
ps [PID]
```

```
top

显示当前系统正在执行的进程的相关信息，包括进程 ID、内存占用率、CPU 占用率等
```

```
free -m -s 10

显示系统内存使用, 缓存使用情况
```

```
df -h
df -l

显示系统的磁盘使用情况
```

```
du -ch /opt

显示文件夹的使用空间情况
```

```
netstat -a

显示所有端口
```

```
ssh
```