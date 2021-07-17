# 常见问题和心得

## Warning Python 3.6 was not found on your system

**背景**：用pipenv去创建和初始化虚拟环境，但是报错：

```bash
# pipenv install
Warning: Python 3.6 was not found on your system
You can specify specific versions of Python with:
  $ pipenv --python path/to/python
```

**错误原因**：此处已有带`Pipfile`是别处（本地Mac）的系统创建的，其Python是`3.6`。当前系统（在线CentOS服务器）Python是`Python 3.4`，没有希望的`Python 3.6`，所以报错。

**解决办法**：

此处解决问题思路是：

* 要么重新安装Mac本地的Python3为Python 3.4，重新弄出pipenv的环境
* 要么重新安装服务器中的Python3为Python 3.6，这样就和本地Mac的Pipfile一致了

不过此处情况稍微有点点特殊：

两种方式都不想做，觉得一是麻烦，二是考虑到目前Python3（Flask的）代码不是很多，Python3.4和Python3.6差异不是很大，至少短期内用起来没有问题

所以打算将就着凑合用：

在服务器端，使用本地Mac中的`Python 3.6`的Pipfile，但是创建出来的`Python 3.4`的虚拟环境

**具体步骤**：

```bash
pipenv install --python 3.4
```

即可。

## The script virtualenv is installed in which is not on PATH

**背景**：

```bash
pip3 install pipenv --user
```

安装后看到警告：

```bash
  The script virtualenv is installed in '/Users/crifan/Library/Python/3.6/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The script virtualenv-clone is installed in '/Users/crifan/Library/Python/3.6/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The scripts pewtwo, pipenv and pipenv-resolver are installed in '/Users/crifan/Library/Python/3.6/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed certifi-2018.4.16 pipenv-11.10.0 virtualenv-15.2.0 virtualenv-clone-0.3.0
```

**原因**：pipenv安装后，默认没有把对应的pipenv（以其他相关的pewtwo，pipenv-resolver，virtualenv，virtualenv-clone）的所在路径

此处是：`/Users/crifan/Library/Python/3.6/bin`，加入到PATH中，这会导致命令行中找不到pipenv（和另外几个）

**解决办法**：按照提示，把上述路径加到PATH中。

**具体步骤**：

把：

```bash
export PATH="/Users/crifan/Library/Python/3.6/bin:$PATH"
```

加到（系统启动脚本）`.bashrc`中

-》为了以后每次启动电脑后，PATH中都包含该路径。

备注：为了当前不重启（终端或系统）就使得PATH生效，所以去：

```bash
source ~/.bashrc
```

然后此刻PATH中即可包含该路径。

-》命令行中就可以找到这些`pipenv`等工具了

-》后续命令行中运行`pipenv`就不会报错找不到了

## 关于如何在pipenv中运行python代码

举例：

```bash
pipenv run python testRestApi.py
```
