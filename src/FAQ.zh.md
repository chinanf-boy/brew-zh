
# 常见问题解答

## 如何更新本地包?

首先更新公式和自制程序:

```
brew update
```

你现在可以发现什么过时了:

```
brew outdated
```

升级一切:

```
brew upgrade
```

或升级一个特定的公式:

```
brew upgrade <formula>
```

## 如何阻止某些公式被更新?

阻止某物被更新/升级:

```
brew pin <formula>
```

允许公式再次更新:

```
brew unpin <formula>
```

注意,另一个公式所依赖的固定过时的公式在需要时需要升级,因为我们不允许针对非最新版本构建公式.

## 如何卸载旧版本的公式?

默认情况下,自制程序不会卸载旧版本的公式,所以随着时间的推移,你会积累旧版本.要删除它们,简单地使用:

```
brew cleanup <formula>
```

或者立刻清理所有的东西:

```
brew cleanup
```

或者看看会清理什么:

```
brew cleanup -n
```

## 如何卸载自制软件?

要卸载自制程序,请在终端提示中粘贴下面的命令.

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
```

下载[卸载脚本](https://raw.githubusercontent.com/Homebrew/install/master/uninstall)并运行`./uninstall --help`查看更多卸载选项.

## 如何卸载公式?

如果不卸载Homebrew已安装的所有版本,Homebrew将继续尝试安装它运行时知道的最新版本`brew upgrade`. 这可能令人惊讶.

要完全删除公式,可以运行`brew uninstall formula_name --force`.

小心,因为这是破坏性的操作.

## 东西下载到哪里去了?

```
brew --cache
```

通常是:`~/Library/Caches/Homebrew`

## 我的麦克`.app`没有找到`/usr/local/bin`公用事业!

GoMac上的GUI应用程序没有`/usr/local/bin`在他们`PATH`默认情况下.如果你在山狮子或以后,你可以通过跑步来解决这个问题.`sudo launchctl config user path "/usr/local/bin:$PATH"`然后重新启动,如文件所示`man launchctl`. 注意,这设置了RunChCTL路径*所有用户*. 对于早期版本的MACOS,请参见[本页](https://developer.apple.com/legacy/library/qa/qa1067/_index.html).

## 我如何为家庭酿造做出贡献?

读[MD的贡献](https://github.com/Homebrew/brew/blob/master/CONTRIBUTING.md).

## 你为什么要编译所有的东西?

自制程序为许多公式提供了预编译版本.这些预编译版本称为[瓶](Bottles.md)并可在[HTTPS://BiTray.COM/HuBrWW/瓶](https://bintray.com/homebrew/bottles).

如果可用,默认情况下将使用瓶装二进制文件,除非在下列条件下:

-   选项被传递到安装命令,即`brew install <formula>`将使用瓶装版本的公式,但`brew install <formula> --enable-bar`将触发源代码生成.
-   这个`--build-from-source`选项被调用.
-   环境变量`HOMEBREW_BUILD_FROM_SOURCE`设置(仅用于开发人员).
-   该机器没有运行支持的MaOS版本,因为所有的瓶装构建都是为支持的MaOS版本生成的.
-   HygBurw安装到标准以外的前缀`/usr/local`(虽然有些瓶子支持这个).

我们的目标是把一切都装满.

## 我如何从别人的分支中得到一个公式?

```sh
brew install hub
brew update
cd $(brew --repository)
hub pull someone_else
```

或:

```
brew pull https://github.com/Homebrew/homebrew-core/pull/1234
```

## 为什么自制啤酒喜欢我安装`/usr/local`?

1.  **更容易**<br>`/usr/local/bin`已经在你的心中`PATH`.
2.  **更容易**<br>如果它们的依赖项不在其中,则生成脚本的数量会减少.`/usr`或`/usr/local`. 我们为Homebrew公式修复了这个问题(虽然我们并不总是测试它),但是您会发现许多RubyGems和Python设置脚本中断,这是我们无法控制的.
3.  **它是安全的**<br>苹果已经为非系统公用事业分配了这个目录.这意味着没有文件在`/usr/local`默认情况下,不必担心弄乱现有或系统工具.

**如果你打算安装依赖于酿造的宝石,那就为自己省下一大堆麻烦,然后安装到`/usr/local`!**

说出来并不总是直截了当的.`gem`查看头文件和库的非标准目录.如果你选择`/usr/local`很多事情都会"工作".

## 为什么家庭酿说SUDO不好?

**DR**Sudo是危险的,不管怎么说,你安装了TutMata.App.

家庭酿拒绝使用SUDO工作.

你只应该做一个你信任的工具.当然,你可以信赖自制软件,但你相信自制程序运行的多兆字节的MaX文件吗?开发人员经常理解C++远远优于理解语法.这太危险了苏多这样的东西.它可以修改(或上载)系统中的任何文件.事实上,我们已经看到一些构建脚本试图修改.`/usr`即使前缀被指定为其他的东西.

我们使用MACOS沙箱来阻止这个,但是当运行时,这不起作用.`root`用户(对系统上几乎所有的事物都有读写访问权限).

是你`chown root /Applications/TextMate.app`?大概不会.所以重要的是`chown root wget`?

如果需要在多用户环境中运行自制程序,请考虑创建单独的用户帐户,尤其是使用自制程序.

## 为什么没有特定的命令记录?

如果不在`man brew`这可能是一个外部命令.这些文件被记录在案.[在这里](External-Commands.md).

## 你为什么不拉我的拉动请求?

如果已经有一段时间了,用一个"颠簸"的评论来撞击它.有时我们错过请求,而且有很多.也许我们在思考什么.这将鼓励考虑.在此期间,如果你可以重新拉拔请求,使它可以樱桃采摘更容易,我们会爱你很长一段时间.

## 我可以自己编辑公式吗?

对!这很容易!只是`brew edit <formula>`. 你不必把修改提交给`homebrew/core`只需根据个人需要编辑公式即可.`brew install`. 作为奖金`brew update`将合并您的更改与上游,所以您仍然可以保持公式最新**具有**你的个人修改!

## 我能做新公式吗?

对!这很容易!只是`brew create URL`. Houb酿将打开公式`EDITOR`所以你可以编辑它,但是它可能已经安装了;试试它:`brew
install <formula>`. 如果遇到任何问题,请使用以下命令运行命令`--debug`开关如下:`brew install --debug <formula>`,这会让您进入调试外壳.

如果你希望你的新配方成为`homebrew/core`或者想更多地了解写作公式,那么请阅读[公式食谱](Formula-Cookbook.md).

## 我能安装我自己的东西吗?`/usr/local`?

对,`brew`被设计成不适合你的方式,所以你可以随心所欲地使用它.

安装您自己的东西,但是要注意,如果您自己安装libexpat等公共库,那么在尝试构建某些Homebrew公式时可能会带来麻烦.因此`brew doctor`会警告你这件事.

因此,最好把自己的东西安装到地窖里.`brew link`它.像这样:

```sh
$ cd foo-0.1
$ brew diy
./configure --prefix=/usr/local/Cellar/foo/0.1
$ ./configure --prefix=/usr/local/Cellar/foo/0.1
[snip]
$ make && make install
$ brew link foo
Linking /usr/local/Cellar/foo/0.1… 17 symlinks created
```

## 为什么公式被删除了?

使用`brew log <formula>`找出答案!可能是因为它有未解决的问题或者我们的分析发现它没有被广泛使用.

## 自制是一个很差的名字,太泛泛了,为什么要选择它呢?

MXCL过于关注啤酒主题,并没有考虑到该项目实际上可能会受到欢迎.当他意识到这一点时,已经太迟了.然而,今天,第一个谷歌击中"自制"不是啤酒有关;

## "KEG"是什么意思?

这意味着公式只装在地窖里,没有链接到里面.`/usr/local`. 这意味着大多数工具找不到它.我们不会因为愚蠢的原因而这样做.如果需要的话,你仍然可以链接到公式中.`brew link`.

## 如何指定公式的不同配置参数?

`brew edit <formula>`并编辑公式.目前没有其他的方法来做到这一点.

## 是否有术语术语表?

你所有的术语需要都可以[在这里找到](Formula-Cookbook.md#homebrew-terminology).
