
## APScheduler 使用步骤
> 快速使用

### 1. 初始化配置

```
scheduler = APScheduler()
scheduler.init_app(app)
scheduler.start()
```

### 2. 添加任务
```
 @scheduler.task('interval', id='interval', seconds=10)
 def scheduled_func():
     print(f"scheduled_func...")
```
### 3. 动态添加任务
```
job_name = 'interval_' + str(datetime.now())
current_app.apscheduler.add_job(func=my_func, id=job_name, trigger="interval", seconds=10)
```

 >组件和参数
 