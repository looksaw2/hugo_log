+++
date = '2025-02-10T18:16:12+08:00'
draft = false
title = '健壮的Python'
+++

### 健壮的Python
首先需要理解为什么需要健壮的Python,首先来看下面的一段代码:
```python
def doubleOp(x):
    return x + x
```
看起来很简单，但是如果使用的人这样调用呢?
```python
x = "Hello World";
x = doubleOp(x)
```
显然的在运行这段程序之后，程序预期的结果和我们预计的不一致,对于数字来说，doubleOp是+1，而对于字符串之类的来说，就是重复两次。这就造成了问题。在例如一个简单的打印:

```python
def printEveryChar(text):
    i = 0;
    while i < len(text):
        print(text[i])
        i += 1
```
和下面的方式比较
```python
def printEveryChar9(text : str) -> None:
    for c in text:
        print(c)
```
显然，下面的方法比较好，更进一步的，可以写出
```python
from typing import Iterable
def printEveryChar(x : Iterable) -> None:
    for c in x:
        print(c)
```
显然，支持的参数类型更多了，可以支持只要是可迭代的类都可以。

### Optional
一个可能包含None值的类型注解 
```python
def parseOptional(x : str) -> Optional[str]:
    return x if x is not None else None;
```

采用Optional[str]其中返回值可能是str或者是None

### 泛型标注
通过Python的TypeVar表示
```python
from typing import TypeVar
T = TypeVar('T')
```
### ToDo

