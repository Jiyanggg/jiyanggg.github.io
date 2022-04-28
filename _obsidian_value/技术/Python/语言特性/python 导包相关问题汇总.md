

### 1. 无法导入项目中其他文件的包

```
- 避免文件夹与文件的名称与第三方的包名重复
- 使用 sys.path 查看当前路径

sys.path.append('/opt/app/project_name')
```