## 修改配置文件
```
cd ~ 
mkdir .pip
ls ~/.pip
sudo gedit ~/.pip/pip.conf
```

```
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host = mirrors.aliyun.com
```

## 临时换源
```
sudo pip3 install <package> -i <url>
```