### 概要

面向对象的文件系统路径操作模块

![pathlib-inheritance.png](/img/bVbBnMH)


> pure paths: 单纯的路径操作，不提供 I/O 操作
> concrete paths: 路径计算操作 + I/O 操作



### 常用的操作

#### 1. 路径的属性

列出所有父目录、父目录、文件名或目录名、文件前缀、文件后缀等...

```python
from pathlib import Path

p = Path('./test/filename.text')

p.parents                 # 所有父目录 
>> WindowsPath.parents

p.parent                  # 父目录
>> test

p.name                    # 文件名或目录名
>> filename.text

p.stem                    # 文件前缀
>> filename

p.suffix                  # 文件后缀
>> .text

p.is_dir()                # 文件夹判断
>> False        

p.is_file()               # 文件判断
>> True

p.exists()                # 路径是否存在
>> True

p.stat()                  # 获取路径属性
>> os.stat_result(st_mode=16895, st_ino=7036874417855445, st_dev=2287178555, st_nlink=1, st_uid=0, st_gid=0, st_size=0, st_atime=1576075587, st_mtime=1576075562, st_ctime=1576075197)

```

#### 2. 路径的操作

创建文件夹、路径连接、写文件、读文件、遍历子路径等...

```python
from pathlib import Path

# 创建文件夹
base_path = Path('dir/child_dir')
base_path.mkdir(exist_ok=True, parents=True)           

# 路径连接
file_path = base_path / Path('file.text')                

# 创建文件
file_path.touch(exist_ok=True)                          

# 写文件
with file_path.open(mode='w', encoding='utf-8') as f:     
    f.write('Hello World')

# 读文件
with file_path.open(mode='r') as f:                       
    print(f.read())

# 遍历子路径
for path in p.iterdir():                                  
    print(path)

# 递归遍历子路径 （正则）
for item in base_path.rglob('*.text'):                   
    print(item)

# 移动文件夹
new_path = base_path / Path('new_file.text')
file_path.replace(new_path)
 
# 删除文件 
new_path.unlink()

# 删除文件夹（必须为空）
new_path.parent.rmdir()
```



### 附录

|         os 和 os.path         |                 pathlib                 |                   说明                    |
| :---------------------------: | :-------------------------------------: | :---------------------------------------: |
|       os.path.abspath()       |             Path.resolve()              |           获取 path 的绝对路径            |
|        os.path.chmod()        |              Path.chmod()               |             改变 path 的权限              |
|        os.path.mkdir()        |              Path.mkdir()               |                创建文件夹                 |
|       os.path.rename()        |              Path.rename()              |                path 重命名                |
|       os.path.replace()       |             Path.replace()              |      path 重命名 (新路径存在则替换)       |
| os.path.remove(), os.unlink() |              Path.unlink()              |                 删除 path                 |
|         os.path.cwd()         |               Path.cwd()                | 当前工作路径（current working directory） |
|       os.path.exists()        |              Path.exists()              |               path 是否存在               |
|     os.path.expanduser()      |            Path.expanduser()            |             path 添加当前用户             |
|        os.path.isdir()        |              Path.is_dir()              |               是否为文件夹                |
|       os.path.isfile()        |             Path.is_file()              |                是否为文件                 |
|       os.path.islink()        |            Path.is_symlink()            |               是否为软链接                |
|           os.stat()           | Path.stat(), Path.owner(), Path.group() |                path 的属性                |
|      os.path.samefile()       |             Path.samefile()             |              是否为相同文件               |
|        os.path.isabs()        |         PurePath.is_absolute()          |              是否为绝对路径               |
|        os.path.join()         |           PurePath.joinpath()           |               路径连接操作                |
|       os.path.dirname()       |             PurePath.parent             |                 前缀路径                  |
|      os.path.basename()       |              PurePath.name              |                 路径名称                  |
|      os.path.splitext()       |             PurePath.suffix             |                 路径后缀                  |

### 参考

[https://docs.python.org/zh-cn/3/library/pathlib.html](https://docs.python.org/zh-cn/3/library/pathlib.html)

[https://xin053.github.io/2016/07/03/pathlib%E8%B7%AF%E5%BE%84%E5%BA%93%E4%BD%BF%E7%94%A8%E8%AF%A6%E8%A7%A3/](https://xin053.github.io/2016/07/03/pathlib%E8%B7%AF%E5%BE%84%E5%BA%93%E4%BD%BF%E7%94%A8%E8%AF%A6%E8%A7%A3/)