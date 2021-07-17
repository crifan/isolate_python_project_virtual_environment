# Python虚拟环境概述

Python项目开发期间，常涉及到不同的Python环境：

* Python版本不同
  * Python的大版本不同：Python2或Python3
  * Python的小版本不同
    * Python2：比如 `Python 2.6`/`Python 2.7`
    * Python3：比如 `Python 3.6`/`Python 3.7`/`Python 3.8`/...
* 每个项目所安装的库的版本不同
  * 比如
    * 某些项目需要某个库的特定的版本：`1.1.0b3`的`sqlalchemy`

## Python虚拟环境工具对比

* `pyvenv`
  * 概述
    * `Python 3.3`和`3.4`中创建虚拟环境的推荐工具
    * 从`Python 3.6`之后
      * 不推荐使用：`pyvenv`
      * 推荐使用：`venv `
* `venv`
  * 概述
    * `Python 3.3`之后，标准库自带的模块，虚拟环境创建和管理工具：`venv`
    * 原理和作用类似于virtualenv，在一定程度上能够替代`virtualenv`
      * 目前来说，社区用`virtualenv`更多，暂时没太多人说要用`venv`取代掉`virtualenv
    * `venv`是`Python3.3`才有的，`Python2.X`不能使用
  * 官网
    * venv — Creation of virtual environments — Python 3.8.2rc1 documentation
      * https://docs.python.org/3/library/venv.html
* `virtualenv`
  * 概述
    * 之前常用的，虚拟环境工具
    * `virtualenv`同时支持`Python2.X`和`Python3.X`
    * 特别是在当前的生产环境中`Python2.X`还占有很大比例的情况下，我们依然需要`virtualenv`
    * virtualenv：很常用的工具，用于创建虚拟环境
    * 隔绝不同项目，使用不同Python环境和版本
    * 官网`PyPA`也很认可
  * `virtualenvwrapper`：一堆的virtualenv的扩展的集合
    * 内含工具
      * `mkvirtualenv`
      * `lssitepackages`
      * `workon`：切换多个虚拟环境
  * `pipenv`
    * 概述
      * [requests](https://book.crifan.com/books/python_summary_http_lib/website/http_thirdparty/requests/)的作者写的
      * 希望把`Pipfile`，`pip`，`virtualenv`集成到一起
      * 
* 另外：Python多版本管理工具
  * `pyenv`
    * 概述
      * 第三方的、开源的多版本`Python`管理工具
      * 用以管理在一台机器上多个`Python`发行版本的共存问题
      * 隔离多个Python版本
      * 比如一台`Linux`机器上同时安装`Python2.7`、`Python3.4`、`Python3.5`三个版本的管理
    * `pyenv-virtualenv`
      * pyenv的插件：同时可以使用pyenv和`virtualenv`
      * `pyenv-virtualenvwrapper`：把`virtualenvwrapper`集成到了`pyenv`

## Python虚拟环境工具结论

* 结论
  * 优先推荐：简单方便好用的 `virtualenv`
  * 其次推荐：locking有点耗时，但也很好用的：`pipenv`
