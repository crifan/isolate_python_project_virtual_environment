# pipenv

* `pipenv`
  * 概述：pipenv是Python虚拟环境管理工具
  * 优点：功能简单易用
  * 缺点
    * locking卡死或耗时很长
      * 历史上（2020年前后），很长一段时间，locking卡死问题，一直没解决，导致几乎不可用
        * 一个简单的`pipenv install xxx`安装可能瞬间就完成，但是后续locking可能要数个小时
      * 最新 20210705，locking问题，基本上解决
        * 现在`pipenv install xxx`后，locking可能要耗时，`几十秒`或者`几分钟`
          * 算还能忍，虽然不爽，但基本可用

## 安装

```bash
pip install pipenv
```

## 使用

* 概述
  * 创建虚拟环境
    ```bash
    pipenv install
    ```
    * 创建虚拟环境+安装库
      ```bash
      pipenv install xxx
      ```
  * 进入虚拟环境
    ```bash
    pipenv shell
    ```
  * 管理库
    * 用`pipenv`或`pip`
      * 用`pipenv`：无需进入虚拟环境，即可去安装和管理库
        ```bash
        pipenv install xxx
        ```
        * 查看已安装库
          ```bash
          pipenv graph
          ```
      * 用`pip`：需要先`pipenv shell`进入虚拟环境，再用`pip`去管理库
        ```bash
        pipenv shell
        pip install xxx
        ```
  * 删除虚拟环境
    ```bash
    pipenv —-rm
    ```

下面详细介绍：

### 创建虚拟环境

```bash
pipenv install
```

举例：

此处是已有Pipfile和Pipfile.lock，然后再去（创建）并进入（恢复）虚拟环境：

```bash
➜  xxx git:(master) ✗ pipenv install
Creating a virtualenv for this project…
Using /usr/local/bin/python3.6m (3.6.4) to create virtualenv…
⠋Running virtualenv with interpreter /usr/local/bin/python3.6m
Using base prefix '/usr/local/Cellar/python/3.6.4_4/Frameworks/Python.framework/Versions/3.6'
New python executable in /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ/bin/python3.6
Also creating executable in /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ/bin/python
Installing setuptools, pip, wheel...done.

Virtualenv location: /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ
Installing dependencies from Pipfile.lock (132fcc)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 29/29 — 00:00:08
```

注意：

install所创建对应的虚拟环境的所在位置是：

`/Users/crifan/.local/share/virtualenvs`

其中crifan是你的用户名

比如：

```bash
➜  xxx git:(master) ✗ ll /Users/crifan/.local/share/virtualenvs
total 0
drwxr-xr-x  8 crifan  staff   256B  4 21 14:47 AutocarData-xI-iqIq4
drwxr-xr-x  7 crifan  staff   224B  5 18 15:58 xxx-SCpLPEyZ
drwxr-xr-x  7 crifan  staff   224B  4 26 16:29 testDownloadChildes-MYpVabF5
➜  xxx git:(master) ✗ ll /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ
total 8
drwxr-xr-x  21 crifan  staff   672B  5 18 15:58 bin
drwxr-xr-x   3 crifan  staff    96B  5 18 15:58 include
drwxr-xr-x   3 crifan  staff    96B  5 18 15:58 lib
-rw-r--r--   1 crifan  staff    61B  5 18 15:58 pip-selfcheck.json
```

### 进入虚拟环境

```bash
pipenv shell
```

举例：

```bash
➜  xxx git:(master) ✗ pipenv shell
Spawning environment shell (/bin/zsh). Use 'exit' to leave.
. /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ/bin/activate
➜  xxx git:(master) ✗ . /Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ/bin/activate
```

进去后，对应的python就是你虚拟环境中的python了：

```bash
➜  xxx git:(master) ✗ which python
/Users/crifan/.local/share/virtualenvs/xxx-SCpLPEyZ/bin/python
```

### 管理Python库

#### 用pipenv管理python库

语法：

```bash
pipenv install xxx
```

举例：

```bash
pipenv install requests

pipenv install pyspider

pipenv install flask-restful

pipenv install mysql
pipenv install mysql-connector-python

pipenv install pymysql

pipenv install openpyxl

pipenv install gunicorn

pipenv install flask-pymongo

pipenv install flask-cors
```

特殊：

* 安装某库(A)，指定所依赖的其他库(B) 
  * 举例
    ```bash
    pipenv install "celery[redis]"
    ```

#### 用pip管理Python库

```bash
pipenv shell

pip install browsermob-proxy
```

注：通过`pip`安装的库，无法自动进入`pipenv`的管理系统的内部逻辑

-》比如`pipenv graph`就无法看到对应的库了

-》就不方便`pipenv`的自动管理已安装的库了

### 查看已安装的库

```bash
pipenv graph
```

举例：

```bash
➜  xxxDemoServer git:(master) ✗ pipenv graph
celery==4.1.0
  - billiard [required: >=3.5.0.2,<3.6.0, installed: 3.5.0.3]
  - kombu [required: <5.0,>=4.0.2, installed: 4.1.0]
    - amqp [required: >=2.1.4,<3.0, installed: 2.2.2]
      - vine [required: >=1.1.3, installed: 1.1.4]
  - pytz [required: >dev, installed: 2018.4]
Flask-Cors==3.0.4
  - Flask [required: >=0.9, installed: 1.0.2]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - Six [required: Any, installed: 1.11.0]
Flask-PyMongo==0.5.1
  - Flask [required: >=0.8, installed: 1.0.2]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - PyMongo [required: >=2.5, installed: 3.6.1]
Flask-RESTful==0.3.6
  - aniso8601 [required: >=0.82, installed: 3.0.0]
  - Flask [required: >=0.8, installed: 1.0.2]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - pytz [required: Any, installed: 2018.4]
  - six [required: >=1.3.0, installed: 1.11.0]
gunicorn==19.8.1
openpyxl==2.5.3
  - et-xmlfile [required: Any, installed: 1.0.1]
  - jdcal [required: Any, installed: 1.4]
PyMySQL==0.8.1
redis==2.10.6
requests==2.18.4
  - certifi [required: >=2017.4.17, installed: 2018.4.16]
  - chardet [required: <3.1.0,>=3.0.2, installed: 3.0.4]
  - idna [required: >=2.5,<2.7, installed: 2.6]
  - urllib3 [required: <1.23,>=1.21.1, installed: 1.22]
```

目的=用途：可以清晰的看出安装了哪些库，每个库的依赖有哪些。

比如我此处关心的：`celery==4.1.0`

举例2：

```bash
# pipenv graph
Flask-Cors==3.0.4
  - Flask [required: >=0.9, installed: 1.0.1]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - Six [required: Any, installed: 1.11.0]
Flask-PyMongo==0.5.1
  - Flask [required: >=0.8, installed: 1.0.1]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - PyMongo [required: >=2.5, installed: 3.6.1]
Flask-RESTful==0.3.6
  - aniso8601 [required: >=0.82, installed: 3.0.0]
  - Flask [required: >=0.8, installed: 1.0.1]
    - click [required: >=5.1, installed: 6.7]
    - itsdangerous [required: >=0.24, installed: 0.24]
    - Jinja2 [required: >=2.10, installed: 2.10]
      - MarkupSafe [required: >=0.23, installed: 1.0]
    - Werkzeug [required: >=0.14, installed: 0.14.1]
  - pytz [required: Any, installed: 2018.4]
  - six [required: >=1.3.0, installed: 1.11.0]
gunicorn==19.8.1
openpyxl==2.5.3
  - et-xmlfile [required: Any, installed: 1.0.1]
  - jdcal [required: Any, installed: 1.4]
PyMySQL==0.8.0
```

### 删除虚拟环境

确保在虚拟环境根目录下，去运行：

```
pipenv --rm
```

举例：

```bash
➜  server pipenv --rm
Removing virtualenv (/Users/crifan/.local/share/virtualenvs/server-9an_1rEM)…
```

## Pipenv的缺点

### 本地和别处Python版本不一致导致代码运行逻辑出错

有时候，由于无法完美复制虚拟环境，（Mac）本地是python 3.6，（CentOS）服务器中是Python 3.4，导致部分语法支持不同，而代码出错：

详见：

【已解决】Python中两个星号**参数去传递给函数出错：SyntaxError invalid syntax

不能完美复制虚拟环境，比如：

本地python 3.6，线上只有python 3.4

造成问题：

1. [【已解决】Python中两个星号**参数去传递给函数出错：SyntaxError invalid syntax](http://www.crifan.com/python_using_two_asterisk_double_star_parameter_function_syntaxerror_invalid_syntax)
2. [【已解决】剧本编写系统Python返回的dict对应的一级topic没有排序](http://www.crifan.com/script_editing_level_one_topic_python_dict_not_sort)


## 附录

### pipenv的help

```bash
➜ pipenv --help
Usage: pipenv [OPTIONS] COMMAND [ARGS]...

Options:
  --where          Output project home information.
  --venv           Output virtualenv information.
  --py             Output Python interpreter information.
  --envs           Output Environment Variable options.
  --rm             Remove the virtualenv.
  --bare           Minimal output.
  --completion     Output completion (to be eval'd).
  --man            Display manpage.
  --three / --two  Use Python 3/2 when creating virtualenv.
  --python TEXT    Specify which version of Python virtualenv should use.
  --site-packages  Enable site-packages for the virtualenv.
  --version        Show the version and exit.
  -h, --help       Show this message and exit.


Usage Examples:
   Create a new project using Python 3.6, specifically:
   $ pipenv --python 3.6

   Install all dependencies for a project (including dev):
   $ pipenv install --dev

   Create a lockfile containing pre-releases:
   $ pipenv lock --pre

   Show a graph of your installed dependencies:
   $ pipenv graph

   Check your installed dependencies for security vulnerabilities:
   $ pipenv check

   Install a local setup.py into your virtual environment/Pipfile:
   $ pipenv install -e .

   Use a lower-level pip command:
   $ pipenv run pip freeze

Commands:
  check      Checks for security vulnerabilities and against PEP 508 markers
             provided in Pipfile.
  clean      Uninstalls all packages not specified in Pipfile.lock.
  graph      Displays currently–installed dependency graph information.
  install    Installs provided packages and adds them to Pipfile, or (if none
             is given), installs all packages.
  lock       Generates Pipfile.lock.
  open       View a given module in your editor.
  run        Spawns a command installed into the virtualenv.
  shell      Spawns a shell within the virtualenv.
  sync       Installs all packages specified in Pipfile.lock.
  uninstall  Un-installs a provided package and removes it from Pipfile.
  update     Runs lock, then sync.
```
