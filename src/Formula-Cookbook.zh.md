
# 公式食谱

公式是用Ruby编写的包定义.它可以用`brew create <URL>`哪里`<URL>`是一个拉链或塔尔球`brew install <formula>`并进行调试`brew install --debug --verbose <formula>`. 公式使用[公式API](http://www.rubydoc.info/github/Homebrew/brew/master/Formula)它提供各种自制的特定助手.

## 家庭酿造术语

| 术语       | 描述                                                                  | 例子                                                                       |
| -------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **公式**   | 包定义                                                                 | `/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/foo.rb` |
| **小桶**   | A的安装前缀**公式**                                                        | `/usr/local/Cellar/foo/0.1`                                              |
| **选择前缀** | 与Active版本的一个链接**小桶**                                                | `/usr/local/opt/foo`                                                     |
| **地窖**   | 所有**小桶**安装在这里                                                       | `/usr/local/Cellar`                                                      |
| **丝锥**   | GIT知识库**公式**和/或命令                                                   | `/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core`                |
| **瓶**    | 预先建造的**小桶**代替源建筑                                                    | `qt-4.8.4.mavericks.bottle.tar.gz`                                       |
| **木桶**   | 安[自制程序的扩展](https://github.com/Homebrew/homebrew-cask)安装Mac OS本地应用程序 | `/Applications/MacDown.app/Contents/SharedSupport/bin/macdown`           |
| **酿造束**  | 安[自制程序的扩展](https://github.com/Homebrew/homebrew-bundle)描述依赖关系       | `brew 'myservice', restart_service: true`                                |

## 引言

HOMBRW使用Git下载更新并为项目做出贡献.

自制程序安装到`Cellar`然后将一些安装符号链接到`/usr/local`以便其他程序可以看到正在发生的事情.我们建议你`brew ls`你的地窖里有几个桶,看看它是怎么排列的.

根据它们的公式,安装软件包.`/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula`. 检查一个简单的例子.`brew edit etl`(或)[etl](https://github.com/Homebrew/homebrew-core/blob/master/Formula/etl.rb)或更高级的`brew edit git`(或)[吉特](https://github.com/Homebrew/homebrew-core/blob/master/Formula/git.rb))

## 基本指令

确保你跑步`brew update`在你开始之前.这将将您的自制程序安装到Git存储库中.

在提交新的公式之前,请确保您的软件包:

-   满足我们所有人[可接受公式](Acceptable-Formulae.md)要求
-   还没有在家酿(检查)`brew search <formula>`)
-   尚未等待合并(检查[问题跟踪器](https://github.com/Homebrew/homebrew-core/pulls))
-   仍然支持上游(即不需要广泛的修补)
-   有一个稳定的标记版本(即不仅仅是一个没有版本的GITHUB存储库)
-   全部通过`brew audit --new-formula <formula>`测验.

在提交一个新的公式之前,一定要仔细阅读.[贡献准则](https://github.com/Homebrew/brew/blob/master/CONTRIBUTING.md).

### 抓取网址

跑`brew create`带有源代码库的URL:

```sh
brew create https://example.com/foo-0.1.tar.gz
```

这创造`/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/foo.rb`打开它`EDITOR`. 看起来会像:

```ruby
class Foo < Formula
  desc ""
  homepage ""
  url "https://example.com/foo-0.1.tar.gz"
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7"

  # depends_on "cmake" => :build

  def install
    # ENV.deparallelize
    system "./configure", "--disable-debug",
                          "--disable-dependency-tracking",
                          "--disable-silent-rules",
                          "--prefix=#{prefix}"
    # system "cmake", ".", *std_cmake_args
    system "make", "install"
  end

  test do
    system "false"
  end
end
```

如果`brew`说`Warning: Version cannot be determined from URL`当做`create`步骤,您需要显式添加正确的[`version`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#version-class_method)然后将公式保存到公式中.

家庭酿将尝试猜测公式的名称从它的URL.如果不能这样做,你可以重写这个.`brew create <URL> --set-name <name>`.

### 填入[`homepage`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#homepage%3D-class_method)

**我们不接受没有公式的公式.[`homepage`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#homepage%3D-class_method)!**

一个SSL/TLS(HTTPS)[`homepage`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#homepage%3D-class_method)优先考虑,如果有的话.

试从[`homepage`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#homepage%3D-class_method)这个公式在[`desc`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#desc%3D-class_method)核对.请注意[`desc`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#desc%3D-class_method)Ripe是用公式名自动添加的.

### 检查生成系统

```sh
brew install --interactive foo
```

现在,您使用一个新的提示符,将TabBar提取到一个临时沙箱中.

检查包裹`README`. 是否安装软件包`./configure`,`cmake`还是别的什么?删除注释`cmake`包使用的行`./configure`.

### 检查依赖关系

这个`README`可能告诉你有关依赖和自制或MACOS可能已经有了它们.您可以检查自制的依赖关系.`brew search`. MACOS附带的一些常见的依赖关系:

-   `libexpat`
-   `libGL`
-   `libiconv`
-   `libpcap`
-   `libxml2`
-   `python`
-   `ruby`

还有很多其他的;检查`/usr/lib`对他们来说.

我们一般不在核心主机复制系统库和复杂的工具,但我们做重复的一些常用工具.

特殊例外是OpenSSL和LBRESL.使用任何东西*应该*使用自制的运输等价物和我们的测试机器人的安装后构建`audit`如果它检测到你没有做过这件事,它会发出警告.

OpBurw的OpenSSL是[`keg_only`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#keg_only-class_method)为了避免冲突与制度,有时公式需要有环境变量设置或特殊配置标志通过定位我们的OpenSSL.你可以看到这个机制在[卡拉夫](https://github.com/Homebrew/homebrew-core/blob/ae2206f3e5bb2a7c0065ae1b164d2d011b85858b/Formula/clamav.rb#L38)公式.通常这是不必要的,因为家庭酿造了我们.[建筑环境](https://github.com/Homebrew/brew/blob/fb3bec8d70d375a97554d4c3fed82ad2332b2191/Library/Homebrew/extend/ENV/super.rb)赞成寻找`keg_only`首先公式.

*重要:* `$(brew --prefix)/bin`不在`PATH`在配方安装过程中.如果在生成时有依赖项,则必须指定它们.`brew`将它们添加到`PATH`或创建一个[`Requirement`](http://www.rubydoc.info/github/Homebrew/brew/master/Requirement).

### 将其他公式指定为依赖项

```ruby
class Foo < Formula
  depends_on "pkg-config"
  depends_on "jpeg"
  depends_on "readline" => :recommended
  depends_on "gtk+" => :optional
  depends_on :x11 => :optional
end
```

字符串(例如)`"jpeg"`)指定公式依赖关系.

符号(例如)`:x11`)指定[`Requirement`](http://www.rubydoc.info/github/Homebrew/brew/master/Requirement)它可以由一个或多个公式、桶或其他系统安装的软件(例如X11)来实现.

杂凑(例如)`=>`)指定一些附加信息的公式依赖项.给定单个字符串键,该值可以采用几种形式:

-   符号(目前之一)`:build`,`:test`,`:optional`或`:recommended`)

    -   `:build`这意味着依赖项是构建时唯一的依赖项,因此当从瓶中安装或列出缺少的依赖项时,可以使用`brew missing`.
        -   `:test`意味着在运行时只需要依赖性.`brew test`.
    -   `:optional`生成隐式`with-foo`选项的公式.这意味着`depends_on "foo" => :optional`用户必须通过`--with-foo`为了使用依赖关系.
    -   `:recommended`生成隐式`without-foo`选项,这意味着默认情况下启用了依赖关系,用户必须通过.`--without-foo`禁用此依赖项.可以使用常规选项语法覆盖默认描述(在这种情况下,选项声明必须在依赖项之前):

        ```ruby
        option "with-foo", "Compile with foo bindings" # This overrides the generated description if you want to
        depends_on "foo" => :optional # Generated description is "Build with foo support"
        ```

我们皱眉[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method)在家庭酿造/自制核心,因为他们没有测试的CI.

### 指定与其他公式的冲突

有时候,公式之间存在着激烈的冲突,它是无法避免或规避的.[`keg_only`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#keg_only-class_method).

小冲突的一个很好的例子[麦德尔斯](https://github.com/Homebrew/homebrew-core/blob/master/Formula/mbedtls.rb)它可以编译并编译一个"hello World"可执行文件.这显然是不必要的.`mbedtls`的功能,与流行的GNU冲突`hello`公式会过分,所以我们只是[移除它](https://github.com/Homebrew/homebrew-core/blob/ae2206f3e5bb2a7c0065ae1b164d2d011b85858b/Formula/mbedtls.rb#L27-L28)在安装过程中.

[pdftohtml](https://github.com/Homebrew/homebrew-core/blob/master/Formula/pdftohtml.rb)提供严重冲突的示例,其中两个公式都提供对功能至关重要的同名二进制文件,因此[`conflicts_with`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#conflicts_with-class_method)优先考虑.

一般来说,[`conflicts_with`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#conflicts_with-class_method)应该是最后的选择.这是一个相当钝的乐器.

无法解决的冲突的句法是:

```ruby
conflicts_with "blueduck", :because => "yellowduck also ships a duck binary"
```

### 公式修正

在自制程序中,我们有时接受不包含版本颠簸的公式更新.这些包括资源更新、新补丁或用公式修复安全性问题.

有时,这些更新需要强制重新编译公式本身或其依赖项,以确保公式继续按预期运行,或者关闭安全问题.这种强制重新编译称为[`revision`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#revision%3D-class_method)并插入下面`homepage`/`url`/`sha256`块.

当一个公式的依赖性对该依赖关系的新版本失败时,它必须接收一个[`revision`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#revision%3D-class_method). 可以看到这样一个失败的例子.[在这里](https://github.com/Homebrew/legacy-homebrew/issues/31195)和修复[在这里](https://github.com/Homebrew/legacy-homebrew/pull/31207).

[`revision`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#revision%3D-class_method)s还用于从系统OpenSSL移动到自带OpenSSL的公式,而不对该公式进行任何其他更改.这确保了用户不被暴露于过时的OpenSSL的潜在安全问题.这样的例子可以在[这种承诺](https://github.com/Homebrew/legacy-homebrew/commit/6b9d60d474d72b1848304297d91adc6120ea6f96).

### 版本方案更改

有时公式的版本方案会改变,使得两个版本之间的直接比较不再产生正确的结果.例如,项目可能是版本`13`然后决定成为`1.0.0`. As `13`翻译成`13.0.0`默认情况下,我们的版本控制系统需要干预.

当一个公式的版本方案无法识别一个新版本作为更新版本时,它必须接收一个[`version_scheme`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#version_scheme%3D-class_method). 这样的例子可以看出.[在这里](https://github.com/Homebrew/homebrew-core/pull/4006).

### 对依赖关系的双重检查

当你已经安装了很多公式时,很容易错过一个共同的依赖关系.您可以仔细检查二进制链接到哪些库`otool`命令(也许您需要使用)`xcrun otool`):

```sh
$ otool -L /usr/local/bin/ldapvi
/usr/local/bin/ldapvi:
/usr/local/opt/openssl/lib/libssl.1.0.0.dylib (compatibility version 1.0.0, current version 1.0.0)
/usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib (compatibility version 1.0.0, current version 1.0.0)
/usr/local/lib/libglib-2.0.0.dylib (compatibility version 4201.0.0, current version 4201.0.0)
/usr/local/opt/gettext/lib/libintl.8.dylib (compatibility version 10.0.0, current version 10.2.0)
/usr/local/opt/readline/lib/libreadline.6.dylib (compatibility version 6.0.0, current version 6.3.0)
/usr/local/lib/libpopt.0.dylib (compatibility version 1.0.0, current version 1.0.0)
/usr/lib/libncurses.5.4.dylib (compatibility version 5.4.0, current version 5.4.0)
/System/Library/Frameworks/LDAP.framework/Versions/A/LDAP (compatibility version 1.0.0, current version 2.4.0)
/usr/lib/libresolv.9.dylib (compatibility version 1.0.0, current version 1.0.0)
/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1213.0.0)
```

### 将GEMS、Python模块、GO项目等指定为依赖项

HOBBURW不包已经打包的语言特定的库.这些应该直接安装在`gem`/`cpan`/`pip`等.

如果正在安装应用程序,则使用[`resource`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#resource-class_method)所有特定语言依赖的S:

```ruby
class Foo < Formula
  resource "pycrypto" do
    url "https://files.pythonhosted.org/packages/60/db/645aa9af249f059cc3a368b118de33889219e0362141e75d4eaf6f80f163/pycrypto-2.6.1.tar.gz"
    sha256 "f2ce1e989b272cfcb677616763e0a2e7ec659effa67a88aa92b3a65528f60a3c"
  end

  def install
    resource("pycrypto").stage { system "python", *Language::Python.setup_install_args(libexec/"vendor") }
  end
end
```

[jrnl](https://github.com/Homebrew/homebrew-core/blob/master/Formula/jrnl.rb)是一个很好的公式的例子.最终结果意味着用户不必使用.`pip`或者Python,可以运行`jrnl`.

[自酿诗人](https://github.com/tdsmith/homebrew-pypi-poet)可以帮助你生成`resource`Python应用程序依赖项的节.

### 安装公式

```sh
brew install --verbose --debug foo
```

`--debug`如果生成失败,将要求您打开交互式shell,这样您就可以尝试找出出错的原因.

检查顶部`./configure`输出.一些配置脚本不识别例如`--disable-debug`. 如果您看到关于它的警告,请从公式中删除选项.

### 向公式中添加一个测试

将有效的测试添加到[`test do`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#test-class_method)方程式的方块.这将由`brew test foo`以及[酿造试验机器人](Brew-Test-Bot.md).

这个[`test do`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#test-class_method)块自动创建并更改运行后删除的临时目录.你可以访问这个[`Pathname`](http://www.rubydoc.info/github/Homebrew/brew/master/Pathname)与[`testpath`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#testpath-instance_method)功能.环境变量`HOME`设置为`testpath`内`test do`块.

我们希望测试不需要任何用户输入,并测试应用程序的基本功能.例如`foo build-foo input.foo`是一个很好的测试(尽管它们被广泛使用)`foo --version`和`foo --help`是糟糕的测试.然而,一个糟糕的测试总比没有测试好.

见[克苏](https://github.com/Homebrew/homebrew-core/blob/master/Formula/cmake.rb)对于一个具有良好测试公式的例子.公式写一个基本`CMakeLists.txt`将文件存入测试目录,然后调用Cmake来生成Maxfile.这个测试检查CMake在基本操作期间不会出现分段错误.另一个很好的例子是[TIYXXML2](https://github.com/Homebrew/homebrew-core/blob/master/Formula/tinyxml2.rb)将一个小型C++源文件写入测试目录,编译并链接到TyyXML2库,最后检查所得到的程序是否成功运行.

### 手册

HOBBURW希望找到手册页`#{prefix}/share/man/...`而不在`#{prefix}/man/...`.

一些软件安装到`man`而不是`share/man`因此,检查输出并添加`"--mandir=#{man}"`到`./configure`如果需要的话.

### 关于命名的速记

把公式命名为项目营销产品.所以它是`pkg-config`不是`pkgconfig`;`sdl_mixer`不是`sdl-mixer`或`sdlmixer`.

唯一的例外是像"Apache蚂蚁"之类的东西.Apache在所有东西前面粘贴"Apache",但是我们使用公式名`ant`. 我们只在实例中包含前缀*侏儒*(因为它是名字的一部分)*自由围棋*(因为每个人都称之为GNU-GO),没有人管它叫"Go"."go"这个词太普通了,它的实现太多了.

如果你不知道名字,检查主页,检查维基百科页面.[迪拜称之为什么](https://www.debian.org/distrib/packages).

当家庭酿已经有一个公式`foo`我们通常不接受用另一个名字替换这个公式的请求.`foo`. 这是为了避免混淆和令人惊讶的用户的期望.

当两个公式共享上游名称时,例如[`AESCrypt`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/aescrypt.rb)和[`AESCrypt`](https://github.com/Homebrew/homebrew-core/blob/master/Formula/aescrypt-packetizer.rb)较新的公式通常必须调整名称以避免与当前公式冲突.

如果你是*仍然*不确定,只是承诺.我们会运用一些专横的规则来做决定.

当导入类时,HOBBURW将需要公式,然后创建类的实例.它通过假设公式名可以直接使用类名转换为类名来实现.`regexp`. 规则很简单:

-   `foo-bar.rb`= >`FooBar`
-   `foobar.rb`= >`Foobar`

因此,如果更改类的名称,还必须重命名文件.文件名应该是小写的,类名应该是严格的CAMELSE等价的,例如公式.`gnu-go`和`sdl_mixer`成为班`GnuGo`和`SdlMixer`,即使他们的名字的一部分是首字母缩写词.

在AN中创建Syrink添加别名`Aliases`目录根目录.

### 审计公式

你可以跑`brew audit --strict --online`测试符合家庭风格的配方.这个`audit`命令包括尾随空白的警告、某些源主机的首选URL以及许多其他样式问题.在提交之前修正这些警告会使每个人的进程更快.

提交给自制程序的新公式应该运行`brew audit --new-formula foo`. 这个命令由Brew Test Bot在新提交上执行,作为自动构建和测试过程的一部分,并且比标准审计突出了更多的潜在问题.

使用`brew info`并检查从URL猜测的版本是否正确.添加显式[`version`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#version-class_method)如果不是.

### 提交

一切都是建立在Git上的,所以贡献是容易的:

```sh
brew update # required in more ways than you think (initializes the brew git repository if you don't already have it)
cd $(brew --repo homebrew/core)
# Create a new git branch for your formula so your pull request is easy to
# modify if any changes come up during review.
git checkout -b <some-descriptive-name>
git add Formula/foo.rb
git commit
```

Git提交消息的标准是:

-   第一行是提交摘要.*50字以下*
-   两个(2)新行,然后
-   彻底解释承诺

在自制程序中,我们喜欢把公式的名字放在前面,像这样:`foobar 7.3 (new formula)`. 这看起来有点疯狂,但是您会发现强迫自己总结承诺会鼓励您保持原子性和简洁性.如果你不能用50-80个字符来概括它,你可能会尝试将两个提交作为一个.为了更全面的解释,请阅读Tim Pope的优秀博客文章,[关于Git提交消息的注释](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).

简单版本更新的首选提交消息格式是`foobar 7.3`而修复是`foobar: fix flibble matrix.`.

确保您参考任何相关的GITHUB问题,例如`Closes #12345`在提交消息中.Homebrew的历史是未来撰稿人在试图理解他们感兴趣的公式的当前状态时首先要考虑的事情.

### 推

现在你只需要把你的承诺推到GITHUB.

如果你还没有叉车回家,[去`homebrew-core`仓库和点击叉按钮](https://github.com/Homebrew/homebrew-core).

如果您已经在GITHUB上分叉了自制程序,那么您可以手动推送(只需确保您已经从`Homebrew/homebrew-core`硕士):

```sh
git push https://github.com/myname/homebrew-core/ <what-you-called-your-branch>
```

现在,[打开拉动请求](https://docs.brew.sh/How-To-Open-a-Homebrew-Pull-Request)为了你的改变.

-   每个提交一个公式;每个公式一个提交
-   保持合并退出请求

## 便利工具

### 消息传递

提供了三个命令,用于向用户显示信息消息:

-   `ohai`一般信息
-   `opoo`警告消息
-   `odie`用于错误消息并立即退出

特别是,在安装前需要进行测试之前.`odie`优雅地跳伞例如:

```ruby
if build.with?("qt") && build.with("qt5")
  odie "Options --with-qt and --with-qt5 are mutually exclusive."
end
system "make", "install"
```

### `bin.install "foo"`

你会在一些公式中看到这样的东西.移动文件`foo`进入公式`bin`目录(目录)`/usr/local/Cellar/pkg/0.1/bin`)并使其成为可执行的(`chmod 0555 foo`)

### [`inreplace`](http://www.rubydoc.info/github/Homebrew/brew/master/Utils/Inreplace)

一个方便的功能,可以编辑文件到位.例如:

```ruby
inreplace "path", before, after
```

`before`和`after`可以是字符串或正则表达式.如果需要在文件中进行多个替换,则应该使用块形式:

```ruby
inreplace "path" do |s|
  s.gsub! /foo/, "bar"
  s.gsub! "123", "456"
end
```

确保修改`s`!此块忽略返回的值.

`inreplace`在修补上游永远不会被接受的东西时,应该使用补丁而不是补丁,例如,使软件的构建系统尊重Homebrew的安装层次结构.如果它同时影响Homebrew和MacPorts(即特定于macOS),则应该将其转换为上游提交的修补程序.

如果需要在A中修改变量`Makefile`而不是使用`inreplace`将它们作为参数传递给`make`:

```ruby
system "make", "target", "VAR2=value1", "VAR2=value2", "VAR3=values can have spaces"
```

```ruby
system "make", "CC=#{ENV.cc}", "PREFIX=#{prefix}"
```

注意值*可以*如果使用多个参数形式,则包含非转义空间.`system`.

## 补片

同时[`patch`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#patch-class_method)ES通常应该避免,有时它们是暂时必要的.

什么时候?[`patch`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#patch-class_method)ing(即修复头文件包含、修复编译器警告等)首先要做的是检查上游项目是否知道该问题.如果没有,请提交bug报告和/或提交您的修补程序以包含.我们有时仍然可以接受您的补丁之前,提交上游,但让球滚动修复上游问题,您减少了时间,我们必须携带补丁左右.

*总是证明一个[`patch`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#patch-class_method)附有代码注释!*否则,没有人知道何时删除补丁是安全的,或者在更新公式时安全地保留它.该评论应包括与上游相关问题的链接.

外部的[`patch`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#patch-class_method)可以使用资源样式块声明ES:

```ruby
patch do
  url "https://example.com/example_patch.diff"
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7"
end
```

条形水准仪`-p1`假设.可以使用符号参数重写:

```ruby
patch :p0 do
  url "https://example.com/example_patch.diff"
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7"
end
```

[`patch`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#patch-class_method)ES可以声明为[`stable`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#stable-class_method),[`devel`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#devel-class_method)和[`head`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#head-class_method)阻碍.注意:总是使用块而不是有条件的,即`stable do ... end`而不是`if build.stable? then ... end`.

```ruby
stable do
  # some other things...

  patch do
    url "https://example.com/example_patch.diff"
    sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7"
  end
end
```

嵌入的(**结束**)补丁可以声明如下:

```ruby
patch :DATA
patch :p0, :DATA
```

在文件末尾包含的补丁数据:

```
__END__
diff --git a/foo/showfigfonts b/foo/showfigfonts
index 643c60b..543379c 100644
--- a/foo/showfigfonts
+++ b/foo/showfigfonts
@@ -14,6 +14,7 @@
…
```

也可以通过传递字符串来嵌入补丁.这使得有可能提供多个嵌入式补丁,而只使其中一些条件.

```rb
patch :p0, "..."
```

在嵌入的修补程序中,字符串`HOMEBREW_PREFIX`用常数的值代替.`HOMEBREW_PREFIX`在应用补丁之前.

### 创建差异

```sh
brew install --interactive --git foo
# (make some edits)
git diff | pbcopy
brew edit foo
```

现在只是粘贴到公式后`__END__`. 而不是`git diff | pbcopy`对于一些编辑来说`git diff >> path/to/your/formula/foo.rb`可能有助于确保修补程序未被触摸(例如,白色空间去除、压痕等).

## 高级公式技巧

如果有什么不清楚,你通常可以通过`grep`乒`$(brew --repo homebrew/core)`目录.如果你认为这会有帮助的话,请提交一个拉的请求来修改这份文件!

### 不稳定版本(不稳定版本)`devel`,`head`)

公式可以指定上游项目的替代下载.[`devel`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#devel-class_method)释放(不稳定但不)`master`/`trunk`或[`head`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#head-class_method)(`master`/`trunk`)

#### `devel`

这个[`devel`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#devel-class_method)通过激活`--devel`用于项目的不稳定版本.它在一个块中指定:

```ruby
devel do
  url "https://foo.com/foo-0.1.tar.gz"
  sha256 "85cc828a96735bdafcf29eb6291ca91bac846579bcef7308536e0c875d6c81d7"
end
```

您可以测试是否`devel`使用规范`build.devel?`.

#### `head`

[`head`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#head-class_method)通过激活的URL`--HEAD`打造发展前沿.指定它是容易的:

```ruby
class Foo < Formula
  head "https://github.com/mxcl/lastfm-cocoa.git"
end
```

家庭自制`git`,`svn`和`hg`URL,并有指定的方式`cvs`储存库也是一个URL.您可以测试是否[`head`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#head-class_method)正在建造中`build.head?`.

若要从存储库中使用特定的提交、标记或分支,请指定[`head`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#head-class_method)与`:tag`和`:revision`,`:revision`或`:branch`选项,像这样:

```ruby
class Foo < Formula
  head "https://github.com/some/package.git", :revision => "090930930295adslfknsdfsdaffnasd13"
                                         # or :branch => "develop" (the default is "master")
                                         # or :tag => "1_0_release",
                                         #    :revision => "090930930295adslfknsdfsdaffnasd13"
end
```

### 编译程序选择

有时在使用某个编译器时无法构建包.最近以来[XCODE版本](Xcode.md)不再包含GCC编译器,我们不能简单地强制使用GCC.相反,正确的声明方法是[`fails_with`DSL方法](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#fails_with-class_method). 适当构造[`fails_with`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#fails_with-class_method)阻止文档编译的最新编译版本,导致编译失败,以及失败的原因.例如:

```ruby
fails_with :clang do
  build 211
  cause "Miscompilation resulting in segfault on queries"
end
```

`build`取一个Fixnum(整数),你可以在你的身上找到这个数字.`brew --config`输出).`cause`采用字符串,并鼓励使用遗传算法来提高可读性,并允许更全面的文档.

[`fails_with`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#fails_with-class_method)声明可用于任何`:gcc`,`:llvm`和`:clang`. HOBPROW将使用此信息来选择工作编译器(如果有可用的编译器).

### 显式指定下载策略

要使用HOBBURW内置下载策略之一,请指定`:using =>`A上的旗帜`url`或`head`.  例如:

```ruby
class Python3 < Formula
  homepage "https://www.python.org/"
  url "https://www.python.org/ftp/python/3.4.3/Python-3.4.3.tar.xz"
  sha256 "b5b3963533768d5fc325a4d7a6bd6f666726002d696f1d399ec06b043ea996b8"
  head "https://hg.python.org/cpython", :using => :hg
```

自制软件提供的下载策略有:

| `:using`价值 | 下载策略                          |
| ---------- | ----------------------------- |
| `:bzr`     | `BazaarDownloadStrategy`      |
| `:curl`    | `CurlDownloadStrategy`        |
| `:cvs`     | `CVSDownloadStrategy`         |
| `:git`     | `GitDownloadStrategy`         |
| `:hg`      | `MercurialDownloadStrategy`   |
| `:nounzip` | `NoUnzipCurlDownloadStrategy` |
| `:post`    | `CurlPostDownloadStrategy`    |
| `:svn`     | `SubversionDownloadStrategy`  |

如果需要对文件的下载和暂存方式进行更多控制,则可以创建自定义下载策略,并使用[`url`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#url-class_method)方法的`:using`选项:

```ruby
class MyDownloadStrategy < SomeHomebrewDownloadStrategy
  # Does something cool
end

class Foo < Formula
  url "something", :using => MyDownloadStrategy
end
```

### 只需移动一些文件

当安装函数中的代码运行时,当前工作目录被设置为提取的TARBARE.

所以只需移动一些文件就容易了:

```ruby
prefix.install "file1", "file2"
```

或一切:

```ruby
prefix.install Dir["output/*"]
```

一般来说,我们更希望您具体需要安装什么文件或目录,而不是安装所有的东西.

#### 目录位置变量

| 名字                    | 违约                                             | 例子                                                |
| --------------------- | ---------------------------------------------- | ------------------------------------------------- |
| **`HOMEBREW_PREFIX`** | `/usr/local`                                   |                                                   |
| **`prefix`**          | `#{HOMEBREW_PREFIX}/Cellar/#{name}/#{version}` | `/usr/local/Cellar/foo/0.1`                       |
| **`opt_prefix`**      | `#{HOMEBREW_PREFIX}/opt/#{name}`               | `/usr/local/opt/foo`                              |
| **`bin`**             | `#{prefix}/bin`                                | `/usr/local/Cellar/foo/0.1/bin`                   |
| **`doc`**             | `#{prefix}/share/doc/foo`                      | `/usr/local/Cellar/foo/0.1/share/doc/foo`         |
| **`include`**         | `#{prefix}/include`                            | `/usr/local/Cellar/foo/0.1/include`               |
| **`info`**            | `#{prefix}/share/info`                         | `/usr/local/Cellar/foo/0.1/share/info`            |
| **`lib`**             | `#{prefix}/lib`                                | `/usr/local/Cellar/foo/0.1/lib`                   |
| **`libexec`**         | `#{prefix}/libexec`                            | `/usr/local/Cellar/foo/0.1/libexec`               |
| **`man`**             | `#{prefix}/share/man`                          | `/usr/local/Cellar/foo/0.1/share/man`             |
| **`man[1-8]`**        | `#{prefix}/share/man/man[1-8]`                 | `/usr/local/Cellar/foo/0.1/share/man/man[1-8]`    |
| **`sbin`**            | `#{prefix}/sbin`                               | `/usr/local/Cellar/foo/0.1/sbin`                  |
| **`share`**           | `#{prefix}/share`                              | `/usr/local/Cellar/foo/0.1/share`                 |
| **`pkgshare`**        | `#{prefix}/share/foo`                          | `/usr/local/Cellar/foo/0.1/share/foo`             |
| **`etc`**             | `#{HOMEBREW_PREFIX}/etc`                       | `/usr/local/etc`                                  |
| **`var`**             | `#{HOMEBREW_PREFIX}/var`                       | `/usr/local/var`                                  |
| **`buildpath`**       | 系统上的临时目录                                       | `/private/tmp/[formula-name]-0q2b/[formula-name]` |

例如,这些代码可以在代码中使用,例如

```ruby
bin.install Dir["output/*"]
```

将二进制文件移动到地窖的正确位置,以及

```ruby
man.mkpath
```

创建手动页位置的目录结构.

要将人页安装到特定位置,请使用`man1.install "foo.1", "bar.1"`,`man2.install "foo.2"`等.

请注意,在自制程序的上下文中,[`libexec`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#libexec-instance_method)由公式保留为私人使用,因此不与`HOMEBREW_PREFIX`.

### 添加可选步骤

如果你想添加一个[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method):

```ruby
class Yourformula < Formula
  ...
  option "with-ham", "Description of the option"
  option "without-spam", "Another description"

  depends_on "foo" => :optional  # will automatically add a with-foo option
  ...
```

然后定义效果[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method)S有:

```ruby
if build.with? "ham"
  # note, no "with" in the option name (it is added by the build.with? method)
end

if build.without? "ham"
  # works as you'd expect. True if `--without-ham` was given.
end
```

[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method)名字应该用词前缀`with`或`without`. 例如,应该运行一个测试套件的选项.`--with-test`或`--with-check`而不是`--test`以及启用共享库的选项`--with-shared`而不是`--shared`或`--enable-shared`.

注意[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method)不是这样的`build.with?`或`build.without?`应该被贬低[`deprecated_option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#deprecated_option-class_method). 见[wget](https://github.com/Homebrew/homebrew-core/blob/master/Formula/wget.rb#L27-L31)举个例子.

我们皱眉[`option`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#option-class_method)在家庭酿造/自制核心,因为他们没有测试的CI.

### 文件级操作

可以使用露比提供的文件实用工具.[`FileUtils`](https://www.ruby-doc.org/stdlib/libdoc/fileutils/rdoc/index.html). 这些都包含在`Formula`类,所以您不需要`FileUtils.`前缀使用它们.

创建链接时,要特别注意确保它们是*相对的*Simulink.这使得更容易创建一个可重新定位的瓶子.例如,在`bin`在一个可执行文件中`libexec`使用

```ruby
bin.install_symlink libexec/"name"
```

而不是:

```ruby
ln_s libexec/"name", bin
```

创建的链接`install_symlink`保证是相对的.`ln_s`当给定相对路径时,只产生相对的链环.

### 处理应遵守公式升级的文件

例如,红宝石1.9的宝石应该安装到`var/lib/ruby/`所以升级宝石时不需要重新安装宝石.你通常可以使用Simulink欺骗,或者*更好的*配置选项.

另一个示例是配置文件,不应在包升级上覆盖.如果安装后发现要持久化,则不复制配置文件,而是*相联的*进入之内`/usr/local/etc/`从地窖中,通常可以通过将适当的参数传递给包的配置脚本来纠正.该参数将根据给定的包的配置脚本和/或MaFag文件而变化,但一个示例可能是:`--sysconfdir=#{etc}`

### 启动文件

HealBurw提供了两个公式方法来启动PLIST文件.[`plist_name`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#plist_name-instance_method)将返回例如`homebrew.mxcl.<formula>`和[`plist_path`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#plist_path-instance_method)将返回例如`/usr/local/Cellar/foo/0.1/homebrew.mxcl.foo.plist`.

## 修正公式

最终,一个新版本的软件将被释放.在这种情况下,您应该更新`url`和`sha256`. 如果A`revision`线存在于任何外部`bottle do`块*和*新版本是稳定的,而不是DEVEL,它应该被删除.

离开`bottle do ... end`我们的CI系统会在我们更改您的更改时更新它.

检查您正在更新的公式是否是通过运行其他公式的依赖项`brew uses UPDATED_FORMULA`. 如果是依赖项,则运行`brew reinstall`对于安装后的所有依赖项,并验证它们是否正确工作.

## 风格指南

HutBurw希望在所有公式的基础上保持一致的红宝石风格.[红宝石风格指南](https://github.com/styleguide/ruby). 其他公式可能还没有更新,以匹配本指南,但所有新的应该.也:

-   公式中的方法的顺序应与其他公式一致(例如:`def install`前行`def post_install`)
-   之前需要一个空行.`__END__`线

## 编写新式公式的疑难解答

### 版本检测失败

自制程序试图自动确定[`version`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#version-class_method)从[`url`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#url-class_method)避免重复.如果TabBar有一个不寻常的名称,您可能需要手动分配[`version`](http://www.rubydoc.info/github/Homebrew/brew/master/Formula#version-class_method).

### 坏文件

并不是所有的项目都有并行运行的文件,所以尝试将这些行添加到`install`方法:

```ruby
ENV.deparallelize
system "make"  # separate make and make install steps
system "make", "install"
```

如果修复了,请打开[问题](https://github.com/Homebrew/homebrew-core/issues)这样我们就可以为每个人解决问题.

### 还是行不通?

看看Mac和Fink做什么:

```sh
brew -S --macports foo
brew -S --fink foo
```

## 超音速音符

`superenv`我们的"超级环境"是通过移除来隔离构建的吗?`/usr/local/bin`以及所有用户`PATH`这对于构建来说不是必需的.这样做是因为用户`PATH`S通常充满了破坏建筑的东西.`superenv`也从传递到的命令中移除坏标记.`clang`/`gcc`注入他人(例如所有)`keg_only`依赖项被添加到`-I`和`-L`标志)

## 福特朗

有些软件需要FORTRAN编译器.这可以通过添加来声明.`depends_on "gcc"`一个公式.

## 如何重新启动(复位到上游)`master`)

您是否创建了一个真正的Git混乱,阻止您创建提交给我们的提交?你可能会考虑从头开始.您的更改可以重置为自制程序.`master`支路运行:

```sh
git checkout -f master
git reset --hard origin/master
```
