
# 公式作者的Python

这个文档解释了如何在一个自制公式中成功地使用Python.

自制程序可以区分Python.**应用**和蟒蛇**图书馆**. 不同之处在于用户通常并不关心应用程序是用Python编写的;用户期望能够`import foo`安装应用程序后.应用实例如下[`ansible`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/ansible.rb)和[`jrnl`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/jrnl.rb).

Python库是由其他Python模块导入的,它们通常是Python应用程序的依赖项.它们通常不受Taleal.App命令行的附带帮助.图书馆的例子[`py2cairo`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/py2cairo.rb)以及安装的绑定[`protobuf --with-python`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/protobuf.rb).

绑定是允许Python代码与用其他语言实现的库或应用程序交互的库的特殊情况.

HypBurw很乐意接受在Python中构建的应用程序,无论应用程序是否从PyPI中获得.自制程序一般不会接受可以正确安装的库.`pip install foo`. 绑定可以为提供它们的包安装,特别是如果PIP没有可用的等效功能.

应用程序应该无条件地捆绑它们的所有Python语言依赖项和库,并且应该安装任何不满意的依赖项;这些策略将在以下部分中深入讨论.

## 应用

### Python声明

需要Python 3的应用程序的公式**应该**声明无条件依赖`"python"`. 这些应用程序**必须**使用当前的自制软件Python 3.x公式.

与Python 2兼容的应用程序**应该**使用苹果提供的系统Python`/usr/bin`在提供Python 2.7的系统上.要做到这一点,声明:

```ruby
depends_on "python@2" if MacOS.version <= :snow_leopard
```

自从最近的OS版本以来,不需要显式的Python依赖性.`/usr/bin`总是在`PATH`对于自制配方,在豹子和老者身上`python`在里面`PATH`如果它至少是版本2.7,或者安装了自制软件的Python 2.7.

### 安装

应用程序应该安装到Python中.[虚拟现实](https://virtualenv.pypa.io/en/stable/)根植于环境`libexec`. 这防止了应用程序的Python模块污染系统站点包,反之亦然.

应用程序的所有Python模块依赖关系(以及它们的依赖性,递归地)都应该声明为`resource`S中的公式,并安装到VielalEnv,以及.每个依赖项都应该明确指定,请不要依赖`setup.py`或`pip`为执行自动依赖性解析,[这里描述的原因](Acceptable-Formulae.md#we-dont-like-install-scripts-that-download-things).

你可以使用[自酿诗人](https://pypi.python.org/pypi/homebrew-pypi-poet)帮助您编写资源节.要使用它,请设置ValueLeNV并安装包及其所有依赖项.然后,`pip install homebrew-pypi-poet`进入同一虚拟时代.运行`poet some_package`将生成必要的资源节.你可以这样做:

```sh
# Install virtualenvwrapper
brew install python
python -m pip install virtualenvwrapper
source $(brew --prefix)/bin/virtualenvwrapper.sh

# Set up a temporary virtual environment
mktmpenv

# Install the package of interest as well as homebrew-pypi-poet
pip install some_package homebrew-pypi-poet
poet some_package

# Destroy the temporary virtualenv you just created
deactivate
```

HOBBRW提供了实例化和填充ValualEnVS的辅助方法.你可以通过放`include Language::Python::Virtualenv`在顶部`Formula`类定义.

对于大多数应用程序,您需要写的是:

```ruby
def install
  virtualenv_install_with_resources
end
```

这与写作完全一样:

```ruby
def install
  # Create a virtualenv in `libexec`. If your app needs Python 3, make sure that
  # `depends_on "python"` is declared, and use `virtualenv_create(libexec, "python3")`.
  venv = virtualenv_create(libexec)
  # Install all of the resources declared on the formula into the virtualenv.
  venv.pip_install resources
  # `pip_install_and_link` takes a look at the virtualenv's bin directory
  # before and after installing its argument. New scripts will be symlinked
  # into `bin`. `pip_install_and_link buildpath` will install the package
  # that the formula points to, because buildpath is the location where the
  # formula's tarball was unpacked.
  venv.pip_install_and_link buildpath
end
```

### 例子

安装依赖关系的公式将是这样的:

```ruby
class Foo < Formula
  include Language::Python::Virtualenv

  url "..."

  resource "six" do
    url "https://pypi.python.org/packages/source/s/six/six-1.9.0.tar.gz"
    sha256 "e24052411fc4fbd1f672635537c3fc2330d9481b18c0317695b46259512c91d5"
  end

  resource "parsedatetime" do
    url "https://pypi.python.org/packages/source/p/parsedatetime/parsedatetime-1.4.tar.gz"
    sha256 "09bfcd8f3c239c75e77b3ff05d782ab2c1aed0892f250ce2adf948d4308fe9dc"
  end

  def install
    virtualenv_install_with_resources
  end
end
```

您还可以使用更冗长的形式,并要求安装特定的资源:

```ruby
def install
  venv = virtualenv_create(libexec)
  %w[six parsedatetime].each do |r|
    venv.pip_install resource(r)
  end
  venv.pip_install_and_link buildpath
end
```

如果你需要为不同的资源做不同的事情.

## 绑定

若要为Python 3添加绑定,请添加`depends_on "python"`.

默认情况下,使用系统Python构建Python 2绑定(不要添加选项),并且它们应该可用于任何二进制兼容的Python.如果情况不是这样,那就是上游错误;[这里有一些解决它的建议](http://blog.tim-smith.us/2015/09/python-extension-modules-os-x/).

### 依赖关系

绑定应遵循与库相同的Python模块依赖性建议;请参阅下面的更多内容.

### 安装绑定

如果绑定是通过调用`setup.py`做一些类似的事情:

```ruby
cd "source/python" do
  system "python", *Language::Python.setup_install_args(prefix)
end
```

如果配置脚本需要`--with-python`标志,它通常不需要额外的帮助找到Python.

如果`configure`和`make`脚本不想安装到地窖中,有时你可以:

1.  呼叫`./configure --without-python`(或者类似的命名选项)
2.  `cd`进入包含Python绑定的目录
3.  呼叫`setup.py`具有`system`和`Language::Python.setup_install_args`(如上所述)

有时我们不得不`inreplace`一`Makefile`使用Python绑定的前缀.(`inreplace`是HOBRUW的助手方法之一,它可以动态地编辑和编辑文本文件.

## 图书馆

### Python声明

为Python 3构建的库应该包括`depends_on "python"`Python 2.x库在安装时必须与系统Python或已生成的Python相对应.

Python 2库不需要`depends_on "python@2"`声明将用系统Python构建,但仍然可以与任何其他Python 2.7一起使用.如果不是这样,它是上游错误;[这里有一些解决它的建议.](http://blog.tim-smith.us/2015/09/python-extension-modules-os-x/).

### 安装

可以将库安装到`libexec`并添加到`sys.path`通过将.pthfile(命名为"HutBurw Fo.pth.")写入`prefix`站点包.这简化了随后的戏剧.`pip`意外地用于升级安装了Homebrew的包,并防止在Homebrew的站点包中累积过时的.pyc文件.

大多数公式目前只安装到`prefix`.

### 依赖关系

必须安装库的依赖关系,以便它们可以导入.为了最小化链接冲突的可能性,应将依赖项安装到`libexec/"vendor"`并添加到`sys.path`通过编写第二个.pthfile(命名为"HutBurw FoApple Reliest.PTH")到`prefix`站点包.

## 再下兔子洞

额外的评论,解释了为什么家庭自制做了一些事情.

### StupTooSvs. diStudisvs PIP

ditudil是Python标准库中的一个模块,它为开发人员提供了一个基本的包管理API.SETUPoToes是分布在标准库之外扩展ditudil的模块.Python软件包提供了一种惯例.`setup.py`那叫`setup()`函数来自ditudil或StudioToots.

提供了`easy_install`命令,它是一个最终用户包管理工具,它从pypy-PythPodePype获取和安装包.`pip`是另一种更新的最终用户包管理工具,它也被提供在标准库之外.PIP植入`easy_install`PIP并没有取代StudioTooCAD模块的其他功能.

ditudil和PIP使用一个"扁平"安装层次结构,它将模块安装为站点包下的单个文件.`easy_install`安装拉链鸡蛋代替现场包装.

分发(不与ditudil混淆)是StupToo工具的过时分支.Distlib是一个在标准库之外维护的包,它由pip用于一些低级包装操作,与大多数包装操作无关.`setup.py`用户.

### 运行`setup.py`

在一个公式需要交互的情况下`setup.py`而不是打电话`pip`家庭自制提供了一种帮手方法,`Language::Python.setup_install_args`为调用返回有用的参数`setup.py`. 你的公式应该使用这个,而不是调用`setup.py`明确地.语法是:

```ruby
system "python", *Language::Python.setup_install_args(prefix)
```

在哪里?`prefix`目的地前缀(通常是`libexec`或`prefix`)

### 是什么`--single-version-externally-managed`?

`--single-version-externally-managed`("sVEM")只是一个StudioToo工具[论证`setup.py install`](https://setuptools.readthedocs.io/en/latest/setuptools.html?#install-run-easy-install-or-old-style-installation). SVEM的主要作用是使用ditudil来执行安装,而不是使用StudioToots.`easy_install`.

`easy_install`做一些我们需要避免的事情:

-   获取和安装依赖项
-   升级依赖项`sys.path`就位
-   PPTH和SIT.PY文件,这些文件对我们不起作用,导致链接冲突.

SETUPoToT需要使用SVEM`--record`提供一个文件列表,这些文件稍后可以用来卸载包.我们不需要或不想要这个,因为自制程序可以管理卸载,但是既然StuuToots需要它,我们就遵从.自制程序的约定是调用记录文件"安装.txt".

检测A是否`setup.py`使用`setup()`从StudioTo工具或ditudil很难,但是我们总是需要把这个标志传递给基于StudioToobe的脚本.`pip`我们面临同样的问题和力量`setup()`使用SETUPoToE版本加载一个垫片`setup.py`在做其他事情之前导入StudioToo工具.自从StUpToo工具猴子补丁ditudil取代它`setup`函数,这提供了一个单一的、一致的接口.我们借用了这个代码并使用它.`Language::Python.setup_install_args`.

### `--prefix` vs `--root`

`setup.py`接受一些令人困惑的安装选项.正确的家庭自制开关`--prefix`,它自动设置`--install-foo`使用Shan-Posi-y值的选项系列.

`--root` [使用](https://mail.python.org/pipermail/distutils-sig/2010-November/017099.html)当安装到不会成为文件最终安装位置的一部分的前缀中时,比如在构建.rpm或二进制发行版时.当使用`setup.py`基于SETUPoTo机,`--root`有副作用`--single-version-externally-managed`. 使用不安全`--root`空着`--prefix`因为`root`当字节编译模块时,从路径中删除.

使用可能是安全的.`--prefix`具有`--root=/`应该使用基于StudioTo工具或ditudil的`setup.py`但是有点难看.

### `pip`VS`setup.py`

[PEP 453](http://legacy.python.org/dev/peps/pep-0453/#recommendations-for-downstream-distributors)向下游经销商(美国)推荐安装SDIST TARPOLL`pip`而不是通过调用`setup.py`直接.我们不这样做是因为苹果的Python分布不包括PIP,所以我们不能假定PIP是可用的.我们可以做一些聪明的事情来解决苹果的困境,但价值主张尚不明确.
