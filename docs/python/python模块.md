---
title: python模块
categories: [技术]
tags: [python]
date: 2023-11-29 11:41:24
---

为了编写可维护的代码，我们把很多函数分组，放到不同的文件中，这样每个文件包含的代码就相对较少，在python中，一个.py文件就称为一个模块(module)。

<!-- more -->

# 模块的概念

模块可以提升代码的可维护性，可以复用代码，避免函数名和变量名冲突等。

为了避免模块名冲突，又引入了包（Package），按照目录来组织模块。比如将模块放到同一个包`mycompany` 下面，这样 `abc.py` 的模块名就变成了 `mycompany.abc`。

每一个包目录下面都会有一个`__init__.py`的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录，而不是一个包，`__init__.py`可以是空文件，也可以有Python代码。

也可以有多级目录，组成多级层次的包结构。

**模块名不要和系统模块名冲突，否则会导致系统模块引入失败。**

# 使用模块

如示例： `hello.py` 文件

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = "张三"

import sys

def test():
    args = sys.argv
    if len(args) == 1:
        print('hello')
    elif len(args)==2:
        print('hello %s' % args[1])
    else:
        print('参数过多')

if __name__ == '__main__':
    test()

```
第1行和第2行是标准注释，第一行可以让该文件在linux下直接运行，第二行注释说明了使用的编码。

第4行是一个字符串，是模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释

第6行使用`__author__`变量把作者写进去

上面就是python模块的标准文件模板。后面开始就是真正的代码部分。

导入`sys`模块后，我们就有了变量`sys`指向该模块，利用`sys`这个变量，就可以访问`sys`模块的所有功能。

最后的两行特殊的代码

```shell
if __name__=='__main__':
    test()
```
在命令行运行`hello`模块文件时，Python解释器把一个特殊变量`__name__`置为`__main__`，而如果在其他地方导入该`hello`模块时，`if`判断将失败，因此，这种if测试可以让一个模块通过命令行运行时执行一些额外的代码，最常见的就是运行测试。


## 作用域

一个模块中，可能有很多的变量和函数，有些函数和变量希望给别人使用，有的函数和变量希望仅仅在模块内部使用，在python中，是通过前缀`_` 实现的。

正常的函数和变量名是公开的(public)， 可以被直接引用，如`abc`，`hello`等。

类似`__xx__`这样的变量是特殊变量，可以被直接引用，但是有特殊的用途。模块的文档注释也可以用`__doc__`变量来访问。我们自己的变量一般不要用这样的变量名。

类似`_xxx`和`__xxx` 这样的变量或者函数就是非公开的(private)，不应该被直接引用。

之所以我们说，private函数和变量“不应该”被直接引用，而不是“不能”被直接引用，是因为Python并没有一种方法可以完全限制访问private函数或变量，但是，从编程习惯上不应该引用private函数或变量。

> 外部不需要引用的函数全部定义成private，只有外部需要引用的函数才定义为public。

# 安装第三方模块

可以通过命令来安装第三方模块。

> pip install xxx

**模块搜索路径**

默认情况下，Python解释器会搜索当前目录、所有已安装的内置模块和第三方模块，搜索路径存放在`sys`模块的`path`变量中：

```shell
>>> import sys
>>> sys.path
['', 'C:\\Python312\\python312.zip', 'C:\\Python312\\DLLs', 'C:\\Python312\\Lib', 'C:\\Python312', 'C:\\Python312\\Lib\\site-packages']
```

如果我们要添加自己的搜索路径，可以设置环境变量 `PYTHONPATH`， 该环境变量的内容会被自动添加到模块搜索路径中。

