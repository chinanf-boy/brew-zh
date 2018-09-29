
# 公式作者节点

该文档说明了如何在基于节点模块的HOBBURW公式中成功地使用节点和NPM.

## 运行`npm install`

HOBBURW提供了两种辅助方法`Language::Node`模块:`std_npm_install_args`和`local_npm_install_args`. 它们既为NPM设置了正确的环境,又为返回参数设置了`npm install`针对他们的具体使用情况.您的公式应该使用这些而不是调用`npm install`明确地.标准节点模块安装的语法是:

```ruby
system "npm", "install", *Language::Node.std_npm_install_args(libexec)
```

哪里`libexec`是目的前缀(通常是`libexec`变量).

## 下载网址

如果Node模块在npm注册表上也是可用的,那么与GitHub(或其他地方)托管的源tarball相比,我们更喜欢npm托管的发布tarballs.这些塔尔球的优点在于它们不包含来自`.npmignore`(如测试)导致较小的下载大小,并且已经完成了任何可能的传输步骤(例如,不需要将CoffeeScript文件编译为构建步骤).

NPM注册表URL通常具有以下格式:

```
https://registry.npmjs.org/<name>/-/<name>-<version>.tgz
```

或者你可以`curl`JSON在`https://registry.npmjs.org/<name>`寻找价值`versions[<version>].dist.tarball`正确的TabBar URL.

## 依赖关系

与最新节点版本兼容的节点模块应该声明依赖于`node`公式.

```ruby
depends_on "node"
```

如果您的公式需要用较旧的节点版本执行,则应该使用版本化的节点公式之一(例如`node@6`)

### 本地插件的特殊要求

如果Node模块是本机addon或在其依赖树中的某个地方有本机addon,则必须声明额外的依赖项.由于本机插件的编译导致调用`node-gyp`我们需要额外的构建时间依赖性.`"python"`(因为GYP依赖于Python 2.7).

```ruby
depends_on "python" => :build
```

还要注意,这样的公式只会与原来编译的同一个节点的主要版本兼容.这意味着我们需要用一个节点本地ADDN来修改每个公式,每个版本的BUMP都是`node`公式.让我们不要忽视你的公式节点上的主要版本的凹凸,写一个有意义的测试,在这种情况下失败(与ABI不兼容版本调用节点).

## 安装

节点模块应该安装到`libexec`. 这防止节点模块污染全局.`node_modules`这是很重要的,所以NPM不尝试管理自制安装的节点模块.

在下面,我们使用公式来区分两种类型的节点模块:

-   与NPM的全局模块格式兼容的标准节点模块的公式[`std_npm_install_args`](#installing-global-style-modules-with-std_npm_install_args-to-libexec)(像[`azure-cli`](https://github.com/Homebrew/homebrew-core/blob/0f3b27d252b8112c744e0460d871cfe1def6b993/Formula/azure-cli.rb)或[`webpack`](https://github.com/Homebrew/homebrew-core/blob/6282879973d569962e63da7c81ac4623e1a8336b/Formula/webpack.rb))
-   公式在哪里`npm install`调用不是唯一需要的安装步骤(例如需要编译非JavaScript源)也必须使用.[`local_npm_install_args`](#installing-module-dependencies-locally-with-local_npm_install_args)(像[`elixirscript`](https://github.com/Homebrew/homebrew-core/blob/4bb491b7b246830aed57b97348a17e9401374978/Formula/elixirscript.rb)

这两种方法的共同特点是,他们使用NPM在自制程序设置正确的环境和返回的参数调用`npm install`针对他们的具体使用情况.这包括用NPM缓存修复一个重要的边缘情况(由HouBurw重定向引起的)`HOME`在构建和测试过程中,通过使用我们自己的习惯`npm_cache`里面`HOMEBREW_CACHE`,否则会造成很长的构建时间和较高的磁盘空间使用率.

要使用它们,必须在公式文件的开头要求节点语言模块:

```ruby
require "language/node"
```

### 安装全局样式模块`std_npm_install_args`到`libexec`

在你的公式中`install`方法,简单`cd`在必要时使用节点模块的顶层,然后使用`system`调用`npm install`具有`Language::Node.std_npm_install_args`像:

```ruby
system "npm", "install", *Language::Node.std_npm_install_args(libexec)
```

这将以NPM的全局模块样式将节点模块安装到自定义前缀中.`libexec`. 所有模块的可执行文件将由NPM自动解决.`libexec/bin`对你来说,这并没有融入到自制软件的前缀中.我们需要确保安装这些设备.要做到这一点,我们需要将所有可执行文件都链接到`bin`用:

```ruby
bin.install_symlink Dir["#{libexec}/bin/*"]
```

**注:**因为需要解决的问题`npm@5`打电话`npm pack`目前我们不支持安装模块(来自非npm注册表tarballs),这需要预发布步骤(例如,用于传输源).见[自制/酿造2820](https://github.com/Homebrew/brew/pull/2820)欲了解更多信息.

### 在本地安装模块依赖项`local_npm_install_args`

在你的公式中`install`方法,做任何安装步骤之前需要做的`npm install`步骤然后`cd`到所包含节点模块的顶层.然后,使用`system`具有`Language::Node.local_npm_install_args`调用`npm install`像:

```ruby
system "npm", "install", *Language::Node.local_npm_install_args
```

这将将所有节点模块依赖项安装到本地生成路径.现在您可以继续您的构建步骤,并将安装安装到自制程序中.`prefix`你自己,跟着[通用自制公式指令](Formula-Cookbook.md).

## 例子

安装基于标准节点模块的公式将是这样的:

```ruby
require "language/node"

class Foo < Formula
  desc "..."
  homepage "..."
  url "https://registry.npmjs.org/foo/-/foo-1.4.2.tgz"
  sha256 "..."

  depends_on "node"
  # uncomment if there is a native addon inside the dependency tree
  # depends_on "python" => :build

  def install
    system "npm", "install", *Language::Node.std_npm_install_args(libexec)
    bin.install_symlink Dir["#{libexec}/bin/*"]
  end

  test do
    # add a meaningful test here
  end
end
```

例如使用`local_npm_install_args`方法查看[`elixirscript`](https://github.com/Homebrew/homebrew-core/blob/ec1e40d37e81af63122a354f0101c377f6a4e66d/Formula/elixirscript.rb)或[`kibana`](https://github.com/Homebrew/homebrew-core/blob/c6202f91a129e2f994d904f299a308cc6fbd58e5/Formula/kibana.rb)公式.

## 工装

你可以使用[自制的NPM NOOB](https://github.com/zmwangx/homebrew-npm-noob)自动生成一个公式,如上面一个NPM包的例子.
