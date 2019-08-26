---
title: Python language Tip
date: 2018-03-05 09:57:42
tags:
- Tip
- Python
---

* 递归/尾递归（在于解释器优化） ！！大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化
* 函数的默认参数： 定义默认参数要牢记一点：默认参数必须指向不变对象！
        可变参数* 关键字参数**
* 切片，迭代，列表生成式（ [x * x for x in range(1, 11)]），
* 生成器（在运行时生成） 
  1. 只要把一个列表生成式的[]改成() next(g)获取！！generator保存的是算法，每次调用next(g)，就计算出g的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。！！
  2. yield **Iterator是惰性计算的序列**
* 高阶函数：传入函数。 map,reduce(累加)  filter sorted

{% codeblock %}
from functools import reduce

DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}

def char2num(s):
    return DIGITS[s]

def str2int(s):
    return reduce(lambda x, y: x * 10 + y, map(char2num, s))
{% endcodeblock %}
* 返回函数（lazy do）
* 匿名函数 lambda x: x * x
* Decorator：decorator就是一个返回函数的高阶函数 @
{% codeblock lang:python %}
# 两层嵌套
import functools

def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
# 三层嵌套
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

@log('execute')
def now():
    print('2015-3-25')
{% endcodeblock %}
* 偏函数

