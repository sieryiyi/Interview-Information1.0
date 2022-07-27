https://www.bilibili.com/video/BV1Vv411x7hj?spm_id_from=333.999.0.0&vd_source=07999cb1d010fa9357b6650a0ee711a7

### 1、Python装饰器

-----原函数-----
```
def func():
    函数过程
    return res
```

！！！在原函数上想要添加新的功能，用闭包、嵌套实现装饰器

！！！当面向批量对若干函数添加功能时，装饰器很好用，维护成本低

##### 改进1.0
```
def outer(origin):
  def inner():
    print("在原函数前加一个输出句子")
    res=origin()----------------------------------这是原函数
    print("在原函数后加一个输出句子")
    return res
    
  return inner
  
  
func=outer(func)
result=func()
print(result)
```

##### 改进2.0

Python中，在某个函数上方，如果使用了@+函数名，则在他的内部，会自动去执行这个函数，且把下面的函数当参数传递进去，再将结果赋值给xxx

```
@函数名
def xxx():
  pass
```
上面一截即xxx=函数名（xxx）

利用上述固定语法，进行简化，简化后为：

```
def outer(origin):
  def inner():
    print("在原函数前加一个输出句子")
    res=origin()----------------------------------这是原函数
    print("在原函数后加一个输出句子")
    return res
    
  return inner

@outer  # 这个语法的意思是执行了func=outer(func)
# 注意，这个函数名要出现在上面，Python是顺序运行的
def func(): 
    函数过程
    res=1
    return res
    
result=func()
print(result)
```

##### 改进3.0

如果本身的func有参数时候的处理方式：用动态参数


```
def outer(origin):
  def inner(*args,**kwargs):
    print("在原函数前加一个输出句子")
    res=origin(*args,**kwargs)----------------------------------这是原函数
    print("在原函数后加一个输出句子")
    return res
    
  return inner

@outer  # 这个语法的意思是执行了func=outer(func)
# 注意，这个函数名要出现在上面，Python是顺序运行的
def func(): 
    函数过程
    res=1
    return res
    
result=func()
print(result)
```

### 2、Python装饰器中的动态参数*args,**kwargs

```
*args：表示无名参数，返回的是元组
**kwargs：表示关键字参数，返回的是字典
```

### 3、常用装饰器

##### functools.lru_cache()

