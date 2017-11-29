代码风格
========

## 代码布局

### 缩进

每个缩进块使用四个空格来缩进。

#### 字典或者函数的多行缩进

+ 函数(TODO)

__疑问:__ 函数是否需要每行一个参数，因为加上注解之后，每个参数很长

```py
def query_online_user_count_statistics(
        start_time, end_time, time_duration):

或者

def query_online_user_count_statistics(start_time,
                                       end_time, time_duration):
```

+ 字典

```py
user = {
    "nickname": signed_dict['nickname'],
    "name": signed_dict['name'],
    "phone": signed_dict['phone'],
    "alipay": signed_dict['alipay'],
    "id_card_photo": signed_dict['id_card_photo'],
    "status": signed_dict['status']
}
```

### 行长度

每行代码最多应该只有79个字符

### 空白行

+ 顶级函数或者顶级类上面应该有两个空白行
+ 类内部定义的方法前面应该有一个空白行
+ 函数内部的逻辑块之间用一个空白行分割

### 源文件编码

+ Python 2代码文件使用 ASCII 编码
+ Python 3代码文件使用 UTF-8 编码

### 模块导入

+ 一条`import`语句应该只导入一个模块，不能导入多个模块

```py
YES: import os
     import sys

NO: import os, sys
```

+ `from XXX import XXX`语句可以一次性导入多个

```py
from subprocess import Popen, PIPE
```

+ 如果从某个模块中导入的属性过多，不应该使用折线进行换行，而应该使用圆括号的方式，每行放一个属性名称:

```py
Good:

from somemodel import (
    class1,
    class2,
    class3,
    class4,
    class5
)

Bad:
from somemodel import class1, class2, class3\
  class4, class5
```

+ 所有的导入语句都应该放在文件的顶部，在文档字符串和注释的后面，在全局的变量和常量定义之前
+ 导入的模块应该按照如下的顺序进行分组

  1. 标准库的导入
  2. 第三方库的导入
  3. 应用程序内部的库或者模块的导入

+ 如果从外部导入的类和本地的类发生了名称冲突，外部的类应该使用模块引用

```py
Bad:

from somemodel.myclass import ConflictClass as NewClass
obj = NewClass()

YES:

from somemodel import myclass
obj = myclass.ConflictClass()
```

+ 通配符导入目前只可以在 Django 的配置继承中使用，其他地方一律禁止使用

  __说明:__ 因为通配符导入会将当前的命名空间混淆，可能会导致某个类或者属性在不知情的情况下被替换

### 模块级别的“dunder”名称

模块基本的“dunder”名称，例如`__all__`, `__version__`, `__author__`应该被放置在文档字符串的后面，除了`from __future__ import XXX`语句之外，所有导入语句的前面。

“dunder”是 __double underscore__ 的缩写，在 Python 中代表一些使用双下划线开头的保留关键字(例如`__all__`, `__version__`, `__author__`等)，参见 [Python Wiki](https://wiki.python.org/moin/DunderAlias)。

```
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

## 字符串引号

+ 所有字符串一律使用双引号
+ 字符串字面值的长度原则上不建议超过最大行长度，长度很长的多行字符串字面值可以用圆括号括起来并换行

```py
usersig = (
    "eJw9z1FvgjAUBeC-Yvq6ZbbFarPEB2MZlshGZGbsiVQp5rIBHdYpMfvvG5ju9XzJPede"
    "0es6eVD7fXOqbWY7o9HjCGF0PxrgW7dHaOo*o5gwQvHE0TH-yJQxkPdIJhhjbzr16D-Do"
    "YfI3y6lL3knOqlP6cubFJ-xNtiZqtwcdLlKeXq265kUy1KMa9wtwF9wQQvvrJ7H72HIdS"
    "ziQAXlUxRGvKl2*AuvNsndpWs4JHLu6iDXtYUCdNu3qryC2tEwMlM289phq8stVMOzhGFC"
    "qTcjzIm*GGh1pgp7O0cYY-TvQfTzC6xQV-E_"
)
```

+ 三引号字符串只可用来做文档字符串
+ 类或者函数内部的注释只可以使用`#`来注释，不可以使用任何形式的字符串来注释

## 表达式和语句中的空白

### 避免使用空格的情况

在下面的一些情况中避免使用空格

+ 在括号，中括号，大括号前后

```py
Yes: spam(ham[1], {eggs: 2})
No:  spam( ham[ 1 ], { eggs: 2 } )
```

+ 在一行代码结尾，是一个逗号跟着关闭括号的时候

```py
Yes: foo = (0,)
No:  bar = (0, )
```

+ 在逗号，冒号和分号的前面

```py
Yes: if x == 4: print x, y; x, y = y, x
No:  if x == 4 : print x , y ; x , y = y , x
```

+ 在一个函数的开括号之前:

```py
Yes: spam(1)
No:  spam (1)
```

+ 在一个列表或者字典的开括号前面:

```py
Yes: dct['key'] = lst[index]
No:  dct ['key'] = lst [index]
```

+ 在赋值语句的等号之前，应该只允许使用一个空格:

```py
Yes:

x = 1
y = 2
long_variable = 3

No:

x             = 1
y             = 2
long_variable = 3
```

+ 然而，存在一些特殊情况，当在一个切片内执行运算的时候，每个运算符前后应该有相同数量的空格:

```
Yes:

ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]  # 注意，当一个运算符的参数被忽略的时候，它两边的空格也应该被忽略
ham[lower + offset : upper + offset]

No:

ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : upper]
ham[ : upper]
```

### 其他建议

+ 在任何时候都不应该保留行尾空白，行尾空白在 Git 的 diff 命令中会使用过红色标记出来
+ 每个运算符的左右都应该有一个空格，这些运算符包括:
  + 赋值: `=`
  + 增加赋值: `+=`, `-=`等一系列运算符
  + 比较运算符: `==`, `<`, `>`, `<=`, `>=`, `in`, `not in`, `is`, `is not`
  + 布尔运算符: `and`, `or`, `not`

+ TODO: 当运算符有不同的级别的时候，尝试在删除高等级运算符周围的空格

```py
Yes:

i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)

No:

i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```

+ 在函数参数的等号赋值周围不要使用空格:

```py
Yes:

def complex(real, imag=0.0):
    return magic(r=real, i=imag)

No:

def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```
+ 函数注解的冒号和普通冒号的规则相同，箭头符号周围应该有空格:

```py
Yes:

def munge(input: AnyStr): ...
def munge() -> AnyStr: ...
No:

def munge(input:AnyStr): ...
def munge()->PosInt: ...
```

+ 当函数的参数既有注解又有默认值的时候，等号周围应该有空格:

```py
Yes:

def munge(sep: AnyStr = None): ...
def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...

No:

def munge(input: AnyStr=None): ...
def munge(input: AnyStr, limit = 1000): ...
```

+ 不允许将多条语句写在一行

```py
Yes:

if foo == 'blah':
    do_blah_thing()
do_one()
do_two()
do_three()

No:

if foo == 'blah': do_blah_thing()
do_one(); do_two(); do_three()
```

## 注释

### 文档字符串

多行文档字符串的格式:

```
"""函数的简短说明

函数的参数或者功能的说明
"""
```

单行文档字符串的格式:

```
"""函数的简短说明"""
```

## 命名规范

### 首要原则

命名应该反映出函数，方法，类，模块等的用途，而不是其实现方式

### 命名风格的建议

+ `_single_leading_underscore`: 没有强制限制的内部标识符
+ `single_trailing_underscore_`: 避免和 Python 关键字冲突，在变量后面添加下划线
+ `__double_leading_and_trailing_underscore__`: "magic" 对象或者方法，例如`__init__`, `__eq__`

### 命名风格的规定

#### 禁止使用

禁止使用`l`, `I`, `O`这样三个单个字母作为变量的名称，因为在一些字体中，他们和1，0难以区分。

如果需要使用`l`作为变量名，可以使用大写的`L`作为替代。

#### ASCII 兼容

必须使用 ASCII 编码内的字符作为标识符的名称（建议字母，数字，下划线）, 不允许使用中文进行命名

#### 包和模块的名称

包和模块的名称应该使用小写字母和下划线组成

如果是用 C/C++ 写的模块应该在前面加上下划线

#### 类的名称

类的名称应该使用大驼峰命名法`MyClass`

#### 类型变量的名称

子定义的类型应该使用大驼峰命名法`MyType`

#### 异常的名称

异常的名称遵循类的命名规范，但应在异常后面加上`Error`的后缀

#### 函数的名称

函数使用小写字母加下划线的命名方式

#### 函数和方法的参数名称

实例方法的第一个参数应该是`self`,不可以改成`this`等其他形式

类方法的第一个参数应该是`cls`, 不可以改成`kls`, `klass`等形式

如果函数的名称和关键字发生冲突，应该在函数后面添加一个下划线

#### 常量的命名

常量应该使用大写字母和下划线命名，应该定义在模块的顶部

#### 继承的设计

+ 如果是计算密集型的操作，不要将其设置为类的属性，类的属性容易让调用者认为这是个非计算密集型操作
