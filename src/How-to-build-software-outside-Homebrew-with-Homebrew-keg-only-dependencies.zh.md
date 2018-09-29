
# 如何用自制软件构建家庭外的软件`keg_only`依赖关系

## "KEG"是什么意思?

这个[常见问题解答](FAQ.md)简单地解释一下.

举个例子:

*OpenSSL没有被链接到我的`PATH`而非自制软件找不到它!*

这是因为Homebrew通常将其锁定在单独的前缀中,而不是与公共可用的位置进行符号链接.`/usr/local`.

## 关于潜在解决方案的建议

在这种情况下,许多人要么有力地联系在一起.`keg_only`工具与`brew link --force`或将默认系统实用程序移出`PATH`并用手工创建的Simulink替换他们提供的自制工具.

*拜托*不要删除Mac OS本地工具,并用SyLink将它们强行替换为自制工具.这样做可能会造成重大破坏,当试图建立软件.

`brew link --force`创建一个警告`brew doctor`让你和维护者都知道可能存在问题的链接.如果你联系了什么,没有任何问题?随意忽略`brew doctor`错误.

## 如何在自制软件之外使用这些工具?

有用的,可靠的替代品存在,如果你想使用`keg_only`自制工具之外的工具.

### 创建标志

您可以设置标志,以便在正确的方向上提供配置脚本或生成文件.标志设置示例:

```sh
./configure --prefix=/Users/Dave/Downloads CFLAGS=-I$(brew --prefix)/opt/openssl/include LDFLAGS=-L$(brew --prefix)/opt/openssl/lib
```

使用实例`pip`:

```sh
CFLAGS=-I$(brew --prefix)/opt/icu4c/include LDFLAGS=-L$(brew --prefix)/opt/icu4c/lib pip install pyicu
```

### `PATH`修改

你可以暂时准备好`PATH`使用工具的bin目录,例如:

```sh
export PATH=$(brew --prefix)/opt/openssl/bin:$PATH
```

这将把文件夹准备好.`PATH`确保搜索的任何构建脚本`PATH`会首先找到它.

改变你`PATH`使用该命令确保该更改只存在于该shell会话的持续时间.一旦你不再参加那个会议,`PATH`恢复到先前状态.

### `pkg-config`侦查

如果正在尝试构建的工具是[PKG配置](https://en.wikipedia.org/wiki/Pkg-config)意识到,你可以修改你的`PKG_CONFIG_PATH`发现`keg_only`公用事业公司`.pc`文件,如果有文件的话.并不是所有的公式都与这些文件相关联.

这样的一个例子是:

```sh
export PKG_CONFIG_PATH=$(brew --prefix)/opt/openssl/lib/pkgconfig
```

如果你对这件事感到好奇`PKG_CONFIG_PATH`变量`man pkg-config`更详细地说.

你可以得到`pkg-config`以以下方式详细说明默认搜索路径:

```sh
pkg-config --variable pc_path pkg-config
```
