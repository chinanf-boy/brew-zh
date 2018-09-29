
# 提示和技巧

## 安装公式以前的版本

支持某些公式的特定版本的安装方法是看是否有版本化的公式(例如`gcc@6`)可用.如果您找的版本不可用,请考虑使用`brew extract`.

### 从拉请求直接安装

你可以[浏览拉动请求](https://github.com/Homebrew/homebrew-core/pulls)并通过直接连接进行安装.例如,Python 3.3.0从拉请求[自制/自制啤酒15199](https://github.com/Homebrew/homebrew/pull/15199):

```sh
brew install https://raw.github.com/dsr/homebrew/9b22d42f50fcbc5e52c764448b3ac002bc153bd7/Library/Formula/python3.rb
```

## 快速去除某物`/usr/local`

```sh
brew unlink <formula>
```

如果一个包不能建立在你链接到的东西的版本上,这可能是有用的.`/usr/local`.

当然,你可以简单地`brew link <formula>`再后来!

## 激活公式的先前安装版本

```sh
brew info <formula>
brew switch <formula> <version>
```

使用`brew info <formula>`若要检查已安装哪些版本,但未激活当前版本,则`brew switch <formula> <version>`激活所需的版本.如果您想在公式的版本之间切换,这可能是有用的.

## 在没有公式的情况下安装到自制程序中

```sh
./configure --prefix=/usr/local/Cellar/foo/1.2 && make && make install && brew link foo
```

## 预先下载一个公式的文件

有时候,通过那些可以作为自制软件的一部分的策略下载文件的速度更快.例如,Erlang提供了一个洪流,可以让你下载4到5×普通HTTP方法.

下载文件并将其放入`~/Library/Caches/Homebrew`,但请注意文件名.自制程序下载文件`<formula>-<version>`. 在Erlang的情况下,这需要重命名文件.`otp_src_R13B03`到`erlang-R13B03`.

`brew --cache -s erlang`将打印缓存下载的正确名称.这意味着不用手动重命名公式,可以运行.`mv the_tarball $(brew --cache -s <formula>)`.

还可以使用命令预缓存下载.`brew fetch formula`它还显示了Sha256哈希.这对于更新公式到新版本是有用的.

## 不使用XCOLL CLT安装数据

```sh
brew sh          # or: eval $(brew --env)
gem install ronn # or c-programs
```

这就进口了`brew`环境进入你现有的外壳;`gem`将拾取环境变量并能够建立.作为奖金`brew`自动设置的优化标志被设置.

## 只安装公式的依赖项(不是公式)

```sh
brew install --only-dependencies <formula>
```

## 互动自制外壳

```sh
$ brew irb
1.8.7 :001 > Formula.factory("ace").methods - Object.methods
 => [:install, :path, :homepage, :downloader, :stable, :bottle, :devel, :head, :active_spec, :buildpath, :ensure_specs_set, :url, :version, :specs, :mirrors, :installed?, :explicitly_requested?, :linked_keg, :installed_prefix, :prefix, :rack, :bin, :doc, :include, :info, :lib, :libexec, :man, :man1, :man2, :man3, :man4, :man5, :man6, :man7, :man8, :sbin, :share, :etc, :var, :plist_name, :plist_path, :download_strategy, :cached_download, :caveats, :options, :patches, :keg_only?, :fails_with?, :skip_clean?, :brew, :std_cmake_args, :deps, :external_deps, :recursive_deps, :system, :fetch, :verify_download_integrity, :fails_with_llvm, :fails_with_llvm?, :std_cmake_parameters, :mkdir, :mktemp]
1.8.7 :002 >
```

## 在完成一个建筑时隐藏啤酒杯表情

```sh
export HOMEBREW_NO_EMOJI=1
```

这就设置了HealBurWyNoyEnJi环境变量,导致自制程序隐藏所有表情符号.

啤酒表情也可以用其他字符代替:

```sh
export HOMEBREW_INSTALL_BADGE="☕️ 🐸"
```

## 编辑器插件

### 崇高文本

在崇高文本2/3中,可以使用包控件来安装[自制公式语法](https://github.com/samueljohn/Homebrew-formula-syntax),它为内嵌补丁添加了高亮显示.

### Vim

[啤酒](https://github.com/xu-cheng/brew.vim)在VIM中增加对内嵌补丁的高亮显示.

### Emacs

[自制模式](https://github.com/dunn/homebrew-mode)为内联修补程序提供语法高亮显示,以及用于编辑公式文件的多个辅助函数.

[自制芯片](https://github.com/hiddenlotus/pcmpl-homebrew)提供Emacs shell模式和ESHELL模式的完成.

### 原子

[语言自制公式](https://atom.io/packages/language-homebrew-formula)添加突出显示和差异支持(与[语言差异](https://atom.io/packages/language-diff)插件).
