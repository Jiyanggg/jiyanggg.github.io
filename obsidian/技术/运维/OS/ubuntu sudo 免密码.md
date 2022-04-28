
`参考链接`:https://www.server-world.info/en/note?os=CentOS_7&p=ceph12&f=1

## 1. 修改文件
```
echo -e 'Defaults:cent !requiretty\ncent ALL = ([user]) NOPASSWD:ALL' | tee /etc/sudoers.d/ceph 
```

## 2.修改权限
```
sudo chmod 440 /etc/sudoers.d/[user]
```

## 3. logout

## 4. login