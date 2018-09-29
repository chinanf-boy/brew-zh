
# 蟒蛇

本页描述了Python是如何在自制程序中为用户处理的.见[公式作者的Python](Python-for-Formula-Authors.md)有关编写公式以安装Python编写的包的建议.

自制应该与任何工作[巨嘴鸟](https://stackoverflow.com/questions/2324208/is-there-any-difference-between-cpython-and-python)默认设置为MyOS系统Python.

HOMBREW提供公式酿造3.x和一个更新的Python 2.7.

**重要:**如果选择安装不是这两者之一的Python(系统Python或酝酿的Python),则Homebrew团队不能支持可能发生的任何破坏.

## Python 3 .x或Python 2 .x

HybBurw为Python 3 .x提供了一个公式.`python`另一个用于Python 2.7.`python@2`)

可执行文件按如下方式组织,使得Python 2和Python 3都可以安装而不冲突:

-   `python3`指向HOBPROW的Python 3 x(如果安装)
-   `python2`指向HOBPROW的Python 2.7 x(如果安装)
-   `python`指向HOBPROW的Python 2.7 .x(如果安装的话),否则MaOS系统Python.退房`brew info python`如果你想添加自制软件的3.`python`对你`PATH`.
-   `pip3`指向HybBurw的Python 3 .x的PIP(如果安装)
-   `pip`和`pip2`指向HOBPROW的Python 2.7 .x的PIP(如果安装)

([不知该选哪一个?](https://wiki.python.org/moin/Python2orPython3))

## StupTooP、PIP等.

Python公式的安装[匹普](http://www.pip-installer.org)(AS)`pip`或`pip2`)[设置工具](https://pypi.python.org/pypi/setuptools).

可以通过PIP更新StudioToo工具,而不必重新编写Python:

```sh
python -m pip install --upgrade setuptools
```

类似地,PIP可以用于通过以下方式来升级自己:

```sh
python -m pip install --upgrade pip
```

### 注`pip install --user`

正常人`pip install --user`为已酿Python禁用.这是因为ditutul中的一个bug,因为自制程序写了一个`distutils.cfg`设置包`prefix`.

一个可能的解决方案(将可执行脚本放入`~/Library/Python/<X>.<Y>/bin`是:

```sh
python -m pip install --user --install-option="--prefix=" <package-name>
```

## `site-packages`以及`PYTHONPATH`

这个`site-packages`是包含Python模块的目录(特别是由其他公式安装的绑定).自制在这里创造:

```sh
$(brew --prefix)/lib/pythonX.Y/site-packages
```

所以,对于python 3 .yz,你会发现它在`/usr/local/lib/python3.y/site-packages`.

Python 3 .y也搜索模块:

-   `/Library/Python/3.y/site-packages`
-   `~/Library/Python/3.y/lib/python/site-packages`

自酿啤酒`site-packages`如果(1)安装了Python绑定的任何自制程序公式,或者(2)`brew install python`.

### 为什么在这里?

这个位置的推理是在Python的(次要)升级或重新安装之间保存您的模块.此外,自制软件有严格的政策,从来不在外面写东西.`brew --prefix`所以我们不会对你的系统进行垃圾邮件.

## 自制程序提供Python绑定

一些公式提供Python绑定.有时一`--with-python`或`--with-python@2`选项必须传递给`brew install`为了构建Python绑定.(检查)`brew options <formula>`)

**警告!**Python可能崩溃(参见[常见问题](Common-Issues.md)如果你`import <module>`从一个酿造的蟒蛇,如果你跑`brew install <formula_with_python_bindings>`反对系统Python.如果您决定切换到酝酿的Python,则用Python绑定重新安装所有公式(例如).`pyside`,`wxwidgets`,`pygtk`,`pygobject`,`opencv`,`vtk`和`boost-python`)

## 非酿造Python绑定策略

这些应该通过`pip install <package>`. 为了发现,你可以使用`pip search`或[HTTPS://PyPI.Python .Org/PyPI](https://pypi.python.org/pypi). (**注:**系统Python不提供`pip`. 跟随[PIP文档](https://pip.readthedocs.io/en/stable/installing/#install-pip)如果你愿意的话,可以为你的系统Python安装它.

## 酿Python模块

对于酝酿的Python,安装了`pip`或`python setup.py install`将安装到`$(brew --prefix)/lib/pythonX.Y/site-packages`目录(上文解释).可执行的Python脚本将在`$(brew --prefix)/bin`.

系统Python可能不知道要设置哪些编译器标志,以便为安装在Homebrew中的软件构建绑定,因此可能需要运行:

```sh
CFLAGS=-I$(brew --prefix)/include LDFLAGS=-L$(brew --prefix)/lib pip install <package>
```

## 虚拟现实

**警告:**当你`brew install`提供Python绑定的公式,您应该**不处于活跃的虚拟环境中**.

激活虚拟现实*之后*你在新的橱窗里酿造或酿造.HybBurw仍然将Python模块安装到自制程序中`site-packages`和*不*进入虚拟环境的站点包.

VielalEnV有一个`--system-site-packages`切换到允许"全局"(即HOBBURW)`site-packages`可以从ValueLeV内部访问.

## 为什么HyBurw的Python被安装为依赖项?

声明无条件依赖的公式`"python"`或`"python@2"`公式被装入自制软件的Python 3 .x或2.7.x,并要求它被安装.
