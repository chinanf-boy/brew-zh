
# 安装

建议的和最简单的安装自制软件的方法是[主页](https://brew.sh).

标准脚本安装自制程序`/usr/local`以便[你不需要苏多](FAQ.md)当你`brew install`. 这是一个谨慎的脚本;即使你安装了一些东西,它也可以运行.`/usr/local`已经.它确切地告诉你它在做之前也会做什么.你必须确认它开始之前所做的一切.

## 要求

-   英特尔CPU<sup>[一](#1)</sup>
-   MACOS 10.12或更高<sup>[二](#2)</sup>
-   Xcode的命令行工具(CLT):`xcode-select --install`,[开发应用程序](https://developer.apple.com/downloads)或[Xcode](https://itunes.apple.com/us/app/xcode/id497799835) <sup>[三](#3)</sup>
-   用于安装的Burne兼容外壳(例如BASH或ZSH)<sup>[四](#4)</sup>

## 替代安装

### OSX狮子10.7及以下

使用指令[HTTPS://BurW.SH](https://brew.sh)或以下任何时候你打电话`curl`你必须通过`--insecure`作为一个论点.这是因为你的系统`curl`太老了,不能用HTTPS和GITHUB说话.别担心,第一`brew update`自制将安装一个更新的,更安全的`curl`为了你的机器.

### 随时随地

只提取(或)`git clone`无论你想要什么,都要自酿.只是避免:

-   包含空格的目录的目录.自制程序可以处理空间,但许多构建脚本不能处理.
-   `/tmp`子目录,因为自制软件会不安
-   `/sw`和`/opt/local`因为构建脚本在自制程序而不是Fink或Mac端口时会变得混乱.

不过,请自己帮忙安装`/usr/local`. 有些东西在其他地方安装时可能无法建立.家庭自制只是相对竞争的原因之一.**因为**我们建议安装到`/usr/local`. *选择另一个前缀在你的危险!*

```sh
mkdir homebrew && curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```

### 多种设施

在提取TabBar的任何地方创建自制程序.无论哪个`brew`命令是安装包的地方.您可以使用这一点,如一个LIBS的系统集.`/usr/local`并调整了公式`~/homebrew`.

## 卸载

卸载记录在[常见问题解答](FAQ.md).

<a name="1"><sup>一</sup></a>不是所有的公式都有CPU或OS要求,但是你可以假设如果你不符合的话你会遇到麻烦.此外,您可以从PoR网络中的其他用户找到PowerPC和老虎分支.见[有趣的水龙头和叉子](Interesting-Taps-and-Forks.md).

<a name="2"><sup>二</sup></a>建议10.12或更高.10.5—10.11是在尽力的基础上支持的.10.4见[虎尾鹦鹉](https://github.com/mistydemeo/tigerbrew).

<a name="3"><sup>三</sup></a>大多数公式需要编译器.少数需要完整的XCODE安装.您可以安装XCODE、CLT,或两者兼备;HOBBRW支持所有三种配置.下载XCODE可能需要苹果开发者帐户上的旧版本的Mac OS X.免费注册.[在这里](https://developer.apple.com/register/index.action).

<a name="4"><sup>四</sup></a>一班轮安装方法发现[啤酒](https://brew.sh)需要一个兼容Burne的shell(例如BASH或ZSH).值得注意的是,鱼类、TCSH和CSH将不起作用.
