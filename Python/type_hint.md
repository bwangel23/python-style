Python 类型注解
==============

## 类型注解语法

Python 类型注解可以标识参数和返回值的类型，PyCharm 可以通过类型注解发现参数或者返回值类型不匹配的情况。同时利用类型注解，也可以让我们模块的接口声明更加明确。

类型注解的语法如下：

```py
def func(arg1: TYPE, arg2: TYPE) -> result: TYPE
    pass
```

在上述的声明中，`TYPE`表示参数或者返回值的类型，具体支持的类型详见下文。

## 基本数据类型

### 系统预置的数据类型

type|说明
---|---
str|字符串类型
int|整数类型
None|空类型
bytes|字节流类型
datetime|时间类型
date|日期类型

### 自定义的数据类型

目前我们的项目中主要是通过枚举来自定义类型，例如性别的定义:

```py

from enum import Enum

class EUserGender(Enum):
    MALE = 'male'
    FEMALE = 'female'
```

通过上面的定义，`EUserGender`也成了一种类型，我们也可以在类型注解中使用`EUserGender`类型。

```py
def create_user(gender: EUserGender) -> dict:
    pass
```

## 复合数据类型

### 列表

`List`表示一个列表,这种类型多用于返回值，表示返回一个列表。

__注意__: 不建议使用列表作为参数，列表是复合类型，可能存在浅拷贝的问题，或者函数内部对于参数的更改影响了外部调用者内变量的值。

`List`的声明方式如下：

```py
def func() -> [int]
```

```py
from typing import List

def func() -> List[int]
```

### 元组

`Tuple`多用于函数返回多个值情况。它的声明方式如下:

```py
from typing import List, Tuple

def func() -> Tuple[int, int]:
   pass

# Tuple 和 List 混合使用
def func() -> Tuple[int, List[int]]:
    pass
```

### 字典

`Dict`可以做返回值或者参数，它的声明方式如下:

```py
# int 表示字典的键的类型，str 表示字典的值的类型
def func1() -> Dict[int, str]:
    return {
        1: 'a'
    }
```

## 其他情况

### Union

有时候我们的方法需要返回多种类型，可以使用`Union`类型来声明。其使用方式如下所示:

```py
from typing import Union

def func1(arg1: int) -> Union[int, None]:
    if arg1 == 0:
        return None
    else:
        return arg1
```
