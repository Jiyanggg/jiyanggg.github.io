```
func = getattr(ClassInstance, 'func_name')
print(func.__code__.co_varnames)
sign = inspect.signature(func)
```