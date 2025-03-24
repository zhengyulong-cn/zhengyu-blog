---
title: Python 语言快速入门
date: 2025-02-20 10:46:06
categories: 
  - 编程技术
tags:
  - Python
---

## 运算符

数值运算：

- 四则运算、`//` 整除、`%`、`**` 幂。

逻辑运算：

- 比较：<、==、>、<=、> =、!=
- 逻辑运算：and、or、not
- 类型转换：int(a)、float(b)、str(a)

海象运算符：在表达式同时进行赋值和返回赋值的值。

```python
if (n := len(a)) > 10:
    print(f"List is too long ({n} elements, expected <= 10)")
```

位运算：

- &（与）、|（或）、^（异或）、~（取反）、<<、> >

成员运算符：

- `in`、`not in`：如果在 **指定序列** 中（没）找到值。

身份运算符：

- `is`、`is not`：判断两个标识符是否引用自一个对象。

> `is` 与 `==` 区别：`is` 用于判断两个变量引用对象是否为同一个， `==` 用于判断引用变量的值是否相等。
>
> ```python
> a = [1, 2, 3]
> b = a
> print(a == b)   # True
> print(a is b)   # True
> b = a[:]
> print(a == b)   # True
> print(a is b)   # False
> ```

## 数据类型

### Number

```python
a, b, c, d = 20, 5.5, True, 4+3j
print(type(a), type(b), type(c), type(d)) # <class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```

1.`int`：表示长整数类型。

2.`bool`：True 为 1，False 为 0。

在 Python3 中，bool 是 int 的子类，可以和数字相互运算。

```python
a = True
b = False
# 逻辑运算符
print(a and b)  # False
print(a or b)   # True
print(not a)    # False
# 类型转换
print(int(a))   # 1
print(float(b)) # 0.0
print(str(a), type(str(a)))   # True <class 'str'>
# 和数字相互运算
print(a + 2)    # 3
```

3.`float`：表示浮点数类型。

```python
# 除法总是返回浮点数
print(14 / 7, 14 // 7)  # 2.0 2
```

4.`complex`：表示复数类型。

### String

字符串是不可变的，因此不能索引赋值和切片赋值。

1.索引：`new_str[1]`。但 **索引越界会报错**。

2.切片：

```python
new_str = "Hello,world!"
# 切片截取
print(new_str[0:2])		# He
print(new_str[:2])		# He
print(new_str[0:-2])	# Hello,worl
# 跨度为2的截取，如果为负数则表示逆向截取
print(new_str[0:-2:2])  # Hlowr
```

3.重复：`new_str * 2`

4.连接：使用 `+` 运算符连接字符串

5.长度：`len(new_str)`

6.f 字符串：

```python
name = "zhengyu"
new_str = f"Hello,{name}!"
print(new_str)	# Hello,zhengyu!
width = 10
precision = 4
value = 12.34567
# 格式化为宽度为width的字符串，并且小数点后保留precision位数字
print(f"result: {value:{width}.{precision}}")	# result:      12.35
```

> 切片操作的第三个参数如果不传入，默认是 1。如果为正，则左闭右开取；如果为负，则左开右闭取。

> 一个很坑的点，python 中有 `str()` 函数，所以变量命名就不能用 `str` 了。

### List

列表是可变的。

1.索引：

```python
list = [1, "Hello", "World", "筝语", "Yotta"]
# 索引获取值
print(list[0])
# 索引赋值
list[0] = "First"
```

2.切片：

```python
list = [1, "Hello", "World", "筝语", "Yotta"]
# 切片截取
print(list[0:3])	# [1, 'Hello', 'World']
print(list[2:])		# ['World', '筝语', 'Yotta']
print(list[-2:])	# ['筝语', 'Yotta']
# 跨度为2的截取
print(list[0:3:2])	# [1, 'World']
# 切片赋值
list[0:2] = ["你好", "世界"]
list[4:] = []
print(list)     # ['你好', '世界', 'World', '筝语']
# 列表置为空
letters[:] = []
```

3.重复：`list* 2`

4.连接：使用 `+` 运算符连接字符串

5.长度：`len(list)`

6.推导式

推导式包含一个表达式，后面为一个 for 子句，然后是零个或多个 for 或 if 子句。

```python
nums = [x for x in range(10)]
print(nums)     # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
pointsList = [(x, y) for x in [1,2,3] for y in [1,2,3] if x != y]
print(pointsList)   # [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
```

### Tuple

元组和列表类似，不同之处在于 **元组的元素不能修改**，写在小括号内 `()`。也可以索引、截取、`+` 操作符拼接。

```python
# 定义元组时，园括号可有可无
tuple1 = 1, 2, 3, 4, 5
tuple2 = (6, 7, 8, 9)
tuple3 = tuple1 + tuple2
# tuple4定义了嵌套的元组
tuple4 = tuple1, tuple2
print(tuple1)   # (1, 2, 3, 4, 5)
print(tuple2)   # (6, 7, 8, 9)
print(tuple3)   # (1, 2, 3, 4, 5, 6, 7, 8, 9)
print(tuple4)   # ((1, 2, 3, 4, 5), (6, 7, 8, 9))
```

### Set

创建集合用花括号 `{}` 或 `set()` 函数创建。

> 注意：创建 **空集合** 只能用 `set()`，不能用 `{}`，因为 `{}` 创建的是空字典。

```python
set1 = {1, "Baidu", 2, "Zhihu", 3, "Bilibili"}
set2 = {4, "Zhihu"}
print(set1)
print(set1 & set2)	# 交集
print(set1 | set2)	# 并集
print(set1 - set2)	# 差集
print(set1 ^ set2)	# 对称差集
```

集合也支持推导式：

```python
a = set(x for x in 'abracadabra' if x in 'abc')
print(a)
```

### Dictionary

创建字典用花括号 `{}` 或 `dict()` 函数创建，字典是无序的 `key:value` 键值对集合。

**键（key）必须使用不可变类型。**

```python
dicts = {
    "name": "P4V列",
    "type": "P4VPath"
}
del dicts["name"]
dicts["property"] = {
    "targetFieldId": "fld28it65nv",
    "closeList": [1, 2, 3],
}
print(dicts)    # {'type': 'P4VPath', 'property': {'targetFieldId': 'fld28it65nv', 'closeList': [1, 2, 3]}}
# 可以用dict()构造函数直接键值对序列创建字典
dicts2 = dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
print(dicts2)   # {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

字典也支持推导式：

```python
dicts = {x: x**2 for x in (2, 4, 6)}
print(dicts)   # {2: 4, 4: 16, 6: 36}
```

### bytes

表示 **不可变的二进制序列**，可以使用 `b` 前缀创建，也可以使用哦个 `bytes()` 函数将其他类型的对象转换为 `bytes` 类型。`bytes()` 函数的第一个参数是要转换的对象，第二个参数是编码方式，如果省略第二个参数，则默认使用 `UTF-8` 编码。

```python
x = bytes("hello", encoding="utf-8")
```

与字符串类型类似，`bytes` 类型也支持许多操作和方法，如切片、拼接、查找、替换等等。同时，由于 `bytes` 类型是不可变的，因此在进行修改操作时需要创建一个新的 `bytes` 对象。

```python
bts = b"Hello"
res = bts[1:3] + b"World"
print(res)		# b'elWorld'
```

## 流程控制

### if...elif...else

```python
import math
def getPowNums(num: int) -> int:
    if num < 0:
        return 0
    elif num >=0 and num <= 10:
        return int(math.pow(num, 2))
    else:
        return 10
```

### for 循环

和其他语言不同，python 中的 for 循环必须以 `for...in...` 使用，**列表、元组、字符串都是序列，是在任意序列的元素上迭代，按它们在序列中出现的顺序**。python 的 for 循环最后可以接 else，循环结束时候会执行。

break 可以跳出 for 和 while，**如果循环终止，对应的 else 不会执行**。continue 可以跳过当此循环块的剩余语句，然后进行下次循环。

`range(start, stop, step)` 函数：返回等差数列的可迭代对象。

```python
print(list(range(5, 10)))       # [5, 6, 7, 8, 9]
print(list(range(0, 10, 3)))    # [0, 3, 6, 9]
print(list(range(0, -10, -2)))  # [0, -2, -4, -6, -8]
```

```python
for i in range(5):
    print(i)
else:
    print("循环结束")
```

### while 循环

```python
count = 0
while count < 5:
   print (count, "小于 5")
   count = count + 1
else:
   print (count, "大于或等于 5")
```

### match...case

基础用法，类似于其它语言的 `switch...case`。

```python
def http_error(status):
    match status:
        case 400|401|402:
            return "客户端请求错误"
        case 500|501|502:
            return "服务端内部错误"
        # 相当于其他语言的default
        case _:
            return "Something's wrong with the internet"
```

高级用法，用到解包和模式匹配。

```python
def process_list(lst):
    match lst:
        case [x, y] if x > 10:
            print(f"两个元素，x大于10：{x} 和 {y}")
        case [x, y] if x <= 10:
            print(f"两个元素，x不大于10：{x} 和 {y}")
        case [x, *rest]:
            print(f"第一个元素：{x}，其余元素：{rest}")
        case []:
            print("空列表")
        case _:
            print("其他情况")

process_list([11, 2])
process_list([10, 2])
process_list([1, 2, 3, 4, 5])
process_list([])
```

### 循环辅助函数

`enumerate()`：返回一个迭代器，迭代器返回元组，元组第一个元素是索引，第二个元素是元素本身。

而字典类型，可以使用字典的方法：

- `dict.keys()`：返回一个迭代器，迭代器返回键构成的列表。
- `dict.items()`：返回一个迭代器，迭代器返回元组，元组第一个元素是键，第二个元素是值。

`zip()`：在多个迭代器上并行迭代，从每个迭代器返回一个数据项组成元组，遍历次数取两者更短的。

```python
new_str = "你好世界"
lists = list([1, 2, 3, 4, 5])
tuples = 1, 2, 3
sets = set(['a', 'b', 'b', 'c', 'a'])
dicts = dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
# 遍历字符串
for ch in new_str:
    print(ch, end=" ")
for index, ch in enumerate(new_str):
    print(f"{index}-{ch}", end=" ")
# 遍历列表或元组
for ch in tuples:
    print(ch, end=" ")
for index, ch in enumerate(lists):
    print(f"{index}-{ch}", end=" ")
# 遍历集合
for ch in sets:
    print(ch, end=" ")
# 遍历字典
for k, v in dicts.items():
    print(f"{k}-{v}", end=" ")
# 组合遍历
for q, a in zip(tuples, dicts.items()):
    print(q, a)
```

## 函数参数

1.默认参数：`def process_list(lst: list = [1, 1])`

> 注意：默认参数虽然能赋值，但最好只拿来用。
>
> 比如下面例子，L 默认参数是空的，但函数会累加后续调用时传递的参数。
>
> ```python
> def f(a, L=[]):
>     L.append(a)
>     return L
> 
> print(f(1))     # [1]
> print(f(2))     # [1, 2]
> print(f(3))     # [1, 2, 3]
> ```
>
> 如果不想后续调用共享默认值，需要这样写：
>
> ```python
> def f(a, L=None):
>     if L is None:
>         L = []
>     L.append(a)
>     return L
> ```

2.关键字参数

函数调用时，可以传入关键字参数，参数名必须与函数定义时参数名一致。

3.可变参数列表和可变关键字参数列表

`def cheeseshop(kind, *arguments, **keywords)` 中，`arguments` 是可变参数列表，元组类型，`keywords` 是可变关键字参数列表，字典类型。

```python
def getPos(x: int, y: int, z: int = 0, *arguments, **keywords) -> None:
    print("x, y, z的值为", [x, y, z])
    print(arguments)
    print(keywords)

getPos(1, 2)
getPos(1, 2, 3, 4, 5)      # arguments为(4, 5)
getPos(z = 1, x = 2, y = 3)
getPos(x = 1, z = 2, y = 3, alpha = 0.5, beta = 0.6)    # keywords为{'alpha': 0.5, 'beta': 0.6}
```

4.解包可变参数列表和解包可变关键字参数列表

用 `*` 把实参从列表或元组解包出来，用 `**` 把实参从字典解包出来。

```python
def getStyle(bold: int, color: str, bgColor: str = "white"):
    print(bold, color, bgColor)

list = [400, 'cyan']
getStyle(*list)     # 400 cyan white
d = { "bold": 500, "color": 'red', "bgColor": 'black' }
getStyle(**d)       # 500 red black
```

5.位置参数和关键字参数的分隔

```bash
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```

在 `/` 前的必须是位置参数，在 `*` 后的必须为关键字参数，两者之间的是两种参数类型都行。


```python
def getPos2(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
    print(pos1, pos2, pos_or_kwd, kwd1, kwd2)

getPos2(pos1 = 1, pos2 = 2, pos_or_kwd = 3, kwd1 = 4, kwd2 = 5)     # TypeError: getPos2() got some positional-only arguments passed as keyword arguments: 'pos1, pos2'
getPos2(1, 2, pos_or_kwd = 3, kwd1 = 4, kwd2 = 5)       # 正常执行
getPos2(1, 2, 3, kwd1 = 4, kwd2 = 5)        # 正常执行
getPos2(1, 2, 3, 4, kwd2 = 5)   # TypeError: getPos2() takes 3 positional arguments but 4 positional arguments (and 1 keyword-only argument) were given
```

5.函数作为实参

函数可以作为实参传递给另一个函数，下面是排序操作的 key 函数例子。

```python
pairs:list[tuple[int, str]] = [(1, 'one'), (3, "three"), (2, 'two')]
def sortDesc(pair):
    return -pair[0]
pairs.sort(key=sortDesc)
```

当然也可以使用 Lambda 表达式。

```python
pairs.sort(key=lambda pair: -pair[0])
```

## 模块和包

### 导入模块

1.导入整个模块：

```python
import module_name
# 使用
module_name.func()
```

2.导入模块函数

```python
# 导入模块特定函数
from module_name import func1, func2
# 导入模块所有函数
from module_name2 import *
# 使用
func1()
func2()
```

3.给模块起别名

```python
import numpy as np
# 使用
a = np.arange(100)
```

### `__all__` 变量

`__all__` 是模块中的一个特殊变量，它定义了模块中应该被导入的内容。当使用 `from module_name import *` 时，只有 `__all__` 指定的内容会被导入。即 `__all__` 限制 `*` 导入的行为。

```python
__all__ = ["echo", "surround", "reverse"]
```

### 模块搜索路径

当导入一个名为 `spam` 的模块时，解释器首先会搜索具有该名称的内置模块。 这些模块的名称在 `sys.builtin_module_names` 中列出。 如果未找到，它将在变量 `sys.path` 所给出的目录列表中搜索名为 `spam.py` 的文件。 `sys.path` 是从这些位置初始化的:

- 被命令行直接运行的脚本所在的目录（或未指定文件时的当前目录）。
- `PYTHONPATH`（目录列表，与 shell 变量 `PATH` 的语法一样）。
- 依赖于安装的默认值（按照惯例包括一个 `site-packages` 目录，由 [`site`](https://docs.python.org/zh-cn/3/library/site.html#module-site) 模块处理）。

> 为了快速加载模块，Python 把模块的编译版本缓存在 `__pycache__` 目录中，文件名为 `module.version.pyc`。

### 包

包是通过使用“带点号模块名”来构造 Python 模块命名空间的一种方式。模块名 `A.B` 表示名为 `A` 的包中名为 `B` 的子模块。

比如有个包目录结构如下：

```
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

导入包时，Python 搜索 `sys.path` 里面的目录，查找包的子目录。

需要有 `__init__.py` 文件才能让 Python 将包含该文件的目录当作包处理。`__init__.py` 可以是空文件，也可以执行包的初始化代码或设置 `__all__` 变量。

`/formats`、`effects/`、`filters/` 是次一级的子包，每个子包中也有 `__init__.py` 文件。

`echo.py` 等文件是子包中的模块，模块中可能包含函数、类或变量。

引用包中的模块：

```python
from sound.effects import echo
```

引用包中子模块的函数或变量：

```python
from sound.effects.echo from echofilter
```

---

如果是 `sound.filters.vocoder` 模块需要使用 `sound.effects` 包中的 echo 模块，可以这样写：

```python
from sound.effects import echo
```

除了以上方式，还可以使用相对导入：

```python
from . import echo
from .. import formats
from ..filters import equalizer
```

## 输入与输出

### f-字符串

整数：

- `:d`：默认整数格式化
- `:<width>d`：右对齐，宽度为 `width`
- `:<0<width>d`：左对齐，宽度为 `width`，用 0 填充空缺
- `:>0<width>d`：右对齐，宽度为 `width`，用 0 填充空缺

浮点数：

- `:.<precision>f`：固定小数点后 `precision` 位。
- `:.<precision>e`：科学计数法表示。

字符串：

- `:<width>.<precision>s`：宽度为 `width`，最多显示 `precision` 个字符。

```python
text = "Hello, world!"
# 左对齐，宽度为20
print(f"文本: {text:<20}")      # 文本: Hello, world!
# 右对齐，宽度为20，最多显示8个字符
print(f"文本: {text:>20.8s}")   # 文本:             Hello, w
```

日期：

| 格式化指令 | 描述                                        |
| ---------- | ------------------------------------------- |
| `%Y`       | 完整的四位数年份，例如 2023                  |
| `%y`       | 不带世纪的两位数年份，例如 23                |
| `%m`       | 月份（01-12）                               |
| `%b`       | 月份的缩写，例如 Jan                         |
| `%B`       | 月份的全称，例如 January                     |
| `%d`       | 一个月中的第几天（01-31）                   |
| `%H`       | 小时（24 小时制，00-23）                     |
| `%I`       | 小时（12 小时制，01-12）                     |
| `%M`       | 分钟（00-59）                               |
| `%S`       | 秒（00-59）                                 |
| `%p`       | AM/PM 标记                                   |
| `%a`       | 星期几的缩写，例如 Mon                       |
| `%A`       | 星期几的全称，例如 Monday                    |
| `%w`       | 星期几（0-6，0 表示周日）                    |
| `%j`       | 一年中的第几天（001-366）                   |

### format()方法

```python
# 花括号中的数字表示传递给str.format()方法的对象所在位置
print('{1} and {0}'.format('生猪', '鸡蛋'))     # 鸡蛋 and 生猪
# 关键字参数
print('{food} is {adjective}'.format(food='苹果', adjective='甜的'))    # 苹果 is 甜的
# 将字典类型解包传入
table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table)) # Jack: 4098; Sjoerd: 4127; Dcab: 8637678
```

### 读写文件

调用 `open()` 函数：

- 第一个传参是文件名字符串；

- 第二个传参是包含描述文件使用方式字符的字符串。
  - `r` ，表示文件只能读取；
  - `w` 表示只能写入（现有同名文件会被覆盖）；
  - `a` 表示打开文件并追加内容，任何写入的数据会自动添加到文件末尾。
  - `r+` 表示打开文件进行读写。
  - 可选参数，省略时的默认值为 `r`。
- 第三个参数是编码形式；

```python
# 读取文件并写入文本
with open('test.txt', 'r+', encoding="utf-8") as f:
    readData = f.read()
    f.write("ddd")
```

> 如果没有使用 `with` 关键字，则应调用 `f.close()` 关闭文件，即可释放文件占用的系统资源。

## 错误和异常

## 类

### 作用域和命名空间

命名空间是从名称到对象的映射，使用 Python 字典实现。

比如下面都是命名空间：

- 内置名称集合
- 模块全局名称
- 函数调用的局部名称
- 对象的属性集合

不同命名空间的名称之间绝对没有关系。

表达式 `z.real` 中，`real` 是对象 `z` 的属性，模块属性和模块中定义的全局名称之间存在直接映射：它们共享相同的命名空间。属性可以只读或可写，模块属性是可写的，即 `modname.the_answer = 42` 写入，也可以使用 `del` 语句删除可写属性，即 `del modname.the_answer`。

内置名称的命名空间是在 Python 解释器启动时创建的，永远不会删除。模块的全局命名空间在读取模块定义时创建。函数的局部命名空间在函数被调用时创建，并在函数返回或抛出未处理的异常时被删除。

一个命名空间的作用域是 Python 代码中的一段文本区域，从这个区域可直接访问该命名空间。

作用域虽然是静态确定的，但会被动态使用。执行期间任何时刻，都会有 3 或 4 个“命名空间可直接访问”的嵌套作用域：

- 最内层的作用域，包含局部名称
- 外层闭包函数的作用域，包含“非局部、非全局”的名称
- 倒数第二层作用域，包含当前模块的全局名称
- 最外层作用域，是内置名称的命名空间

如果一个名称被声明为全局，则所有引用和赋值都将直接指向“倒数第二层作用域”，即包含模块的全局名称的作用域。要重新绑定在最内层作用域以外找到的变量，可以使用 `nonlocal` 语句；如果未使用 `nonlocal` 声明，这些变量将为只读。

作用域是按字面文本确定的：**模块内定义的函数的全局作用域就是该模块的命名空间，无论该函数从什么地方或以什么别名被调用。** 另一方面，实际的名称搜索是在运行时动态完成的。但是，Python 正在朝着“编译时静态名称解析”的方向发展，因此不要过于依赖动态名称解析！

`global` 语句用于表明特定变量在全局作用域里，并应在全局作用域中重新绑定；`nonlocal` 语句表明特定变量在外层作用域中，并应在外层作用域中重新绑定。

```python
def scope_test():
    def do_local():
        spam = "本地的spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "全局的spam"

    spam = "默认的spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
"""
After local assignment: 默认的spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: 全局的spam
"""
```

### 类的基本语法

为了保证所有实例定义的变量各自独立，初始化要在 `__init__` 函数中定义，在外面定义的变量会在不同实例之间共享。基本类型是可以在外面定义的，但如 list、tuple、set、dict 等类型是不能的。

```python
class Dog:
    # 基本类型可以在这里定义
    name = ''
    # 私有变量
    __secretCount = 0
    # 此处定义的tricks不应该被用作类变量，因为所有Dog实例将只共享一个单独的列表
    # tricks = []
    def __init__(self, name):
        self.name = name
        self.tricks = []

    def add_trick(self, trick):
        self.tricks.append(trick)

# 初始化实例
d = Dog('Fido')
e = Dog('Buddy')
# 调用实例方法
d.add_trick('roll over')
e.add_trick('play dead')
# 访问实例属性
print(d.name, d.tricks) # Fido ['roll over']
print(e.name, e.tricks) # Buddy ['play dead']
```

> `self` 代表的是类的实例，而非类

### 继承

Python 支持多继承，当冲突时候，取第一个继承类。

```python
class People:
    name = ''
    age = 0
    __weight = 0
    def __init__(self,n,a,w):
        self.name = n
        self.age = a
        self.__weight = w
    def speak(self):
        print(f'{self.name}说：我{self.age}岁了；体重：{self.__weight}kg')

class Speaker():
    topic = ''
    name = ''
    def __init__(self,n,t):
        self.name = n
        self.topic = t
    def speak(self):
        print(f'我叫{self.name}，我是一个演说家，我演讲的主题是{self.topic}')

class Student(People, Speaker):
    grade = ''
    def __init__(self,n,a,w,g,t):
        #调用父类的构造函数
        People.__init__(self,n,a,w)
        #调用父类的构造函数
        Speaker.__init__(self,n,t)
        self.grade = g
    # 重写父类的方法
    def speak(self):
        print(f'我叫{self.name}，我是一个学生，我演讲的主题是{self.topic}，我读{self.grade}年级')

s = Student('ken', 10, 60, 3, "Python")
s.speak()
```

比如上面代码，如果子类 Student 没有重写 speak 方法，那么调用的是 People 类的 speak 方法，如果继承时写成 `class Student(Speaker, People)`，那么调用的是 Speaker 类的 speak 方法。

可以通过 `super()` 函数调用父类的一个方法：

```python
super(Student, s).speak()
```

### 类专有方法

- `__init__`：构造函数，生成对象时调用
- `__del__`：析构函数，释放对象时调用
- `__repr__`：打印，转化
- `__setitem__`：按照索引赋值
- `__getitem__`：按照索引取值
- `__len__`：获取长度
- `__cmp__`：比较运算
- `__add__`：加法运算
- `__sub__`：减运算
- `__mul__`：乘运算
- `__truediv__`：除运算
- `__mod__`：求余运算
- `__pow__`乘方
- `__iter__`：迭代器
- `__next__`：迭代器下一个值

```python
class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b
 
   def __str__(self):
      return 'Vector (%d, %d)' % (self.a, self.b)
   
   def __add__(self,other):
      return Vector(self.a + other.a, self.b + other.b)
 
v1 = Vector(2,10)
v2 = Vector(5,-2)
print(v1 + v2)		# Vector(7,8)
```

使用类迭代器的例子：

```python
class Reverse:
    def __init__(self, data):
        self.data = data
        self.index = len(data)
    def __iter__(self):
        return self
    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
rev = Reverse("spam")
for char in rev:
    print(char, end=",")
# m,a,p,s,
```





