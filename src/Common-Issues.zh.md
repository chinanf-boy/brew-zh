
# 常见问题

这是一个常见的问题列表,已知的问题,以及它们的解决方案.

### `brew`抱怨"命令行工具"缺失

您需要安装(更新)XCODE命令行实用程序:运行`xcode-select --install`在终端.(在10.9之前的OS X中,"命令行工具"包可以从xCu码内部安装.`⌘,`会给你带来偏好.访问"下载"选项卡,点击"命令行工具"旁边的安装按钮.

### 红宝石:`bad interpreter: /usr/bin/ruby^M: no such file or directory`

你克隆了`git`并且您的Git配置被设置为使用Windows行结束.请参阅本页:[HTTPS://Help](https://help.github.com/articles/dealing-with-line-endings)

### 红宝石:`bad interpreter: /usr/bin/ruby`

你没有`/usr/bin/ruby`或者它不是可执行的.不建议让这种情况持续下去,你会惊讶多少`.app`S,工具和脚本希望你的Mac OS提供的文件和目录是*未修改的*因为安装了MACOS.

### `brew update`对未跟踪的工作树文件的抱怨

运行后`brew update`您将收到关于未跟踪文件或本地更改的Git错误警告,这些文件或本地更改将由签出或合并覆盖,然后是Homebrew安装内的文件列表.

这是由一个老臭虫引起的.`update`早已固定的代码.但是,bug的本质要求您做如下操作:

```sh
cd $(brew --repository)
git reset --hard FETCH_HEAD
```

如果`brew doctor`仍然抱怨未提交的修改,也运行这个命令:

```sh
cd $(brew --repository)/Library
git clean -fd
```

### 红宝石:`invalid multibyte escape: /^\037\213/`

你看到类似的错误:

```
Error: /usr/local/Library/Homebrew/download_strategy.rb:84: invalid multibyte escape: /^\037\213/
invalid multibyte escape: /^\037\235/
```

在过去,自酿假设`/usr/bin/ruby`是红宝石1.8.在OS X 10.9上,它现在是Ruby 2.这两个版本之间存在各种不兼容性,因此如果您在使用足够旧的Homebrew版本时升级到OS X 10.9,则会遇到错误.

在最近版本的自制程序中已经解决了不兼容性,而不是假设.`/usr/bin/ruby`它使用MACOS的Ruby框架内的可执行文件或被渲染的Ruby.

要从这种情况中恢复过来,请做以下几点:

```sh
cd $(brew --prefix)
git fetch origin
git reset --hard FETCH_HEAD
brew update
```

### `launchctl`拒绝加载启动PLIST文件

当试图将一个PLIST文件加载到RunCHCTL中时,会收到类似的错误.

```
Bug: launchctl.c:2325 (23930):13: (dbfd = open(g_job_overrides_db_path, [...]
launch_msg(): Socket is not connected
```

或

```
Could not open job overrides database at: /private/var/db/launchd.db/com.apple.launchd/overrides.plist: 13: Permission denied
launch_msg(): Socket is not connected
```

这可能是由于四个问题之一:

1.  您使用的是迭代.解决方案是使用Teleal.App与之交互.`launchctl`.
2.  您使用的是终端复用器,例如`tmux`或`screen`. 你应该和`launchctl`从一个单独的终端应用程序外壳.
3.  您正在尝试运行`launchctl`远程登录时.您应该启用远程机器上的屏幕共享,并使用在该机器上运行的Teleal.App发出命令.
4.  你是`su`作为一个不同的用户.

### `brew upgrade`错误出

跑步时`brew upgrade`你看到这样的事情:

```
$ brew upgrade
Error: undefined method `include?' for nil:NilClass
Please report this bug:
    https://docs.brew.sh/Troubleshooting
/usr/local/Library/Homebrew/formula.rb:393:in `canonical_name'
/usr/local/Library/Homebrew/formula.rb:425:in `factory'
/usr/local/Library/Contributions/examples/brew-upgrade.rb:7
/usr/local/Library/Contributions/examples/brew-upgrade.rb:7:in `map'
/usr/local/Library/Contributions/examples/brew-upgrade.rb:7
/usr/local/bin/brew:46:in `require'
/usr/local/bin/brew:46:in `require?'
/usr/local/bin/brew:79
```

这是因为旧版本的升级命令由于某种原因而四处徘徊.修复:

```sh
cd $(brew --repository)/Library/Contributions/examples
git clean -n # if this doesn't list anything that you want to keep, then
git clean -f # this will remove untracked files
```

### Python:EasyStudio.PTH不能链接

```
Warning: Could not link <formula>. Unlinking...
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
You can try again using `brew link <formula>'

Possible conflicting files are:
/usr/local/lib/python2.7/site-packages/site.py
/usr/local/lib/python2.7/site-packages/easy-install.pth
==> Could not symlink file: /homebrew/Cellar/<formula>/<version>/lib/python2.7/site-packages/site.py
Target /usr/local/lib/python2.7/site-packages/site.py already exists. You may need to delete it.
To force the link and overwrite all other conflicting files, do:
  brew link --overwrite formula_name

To list all files that would be deleted:
  brew link --overwrite --dry-run formula_name
```

不要听从建议,而是用`Language::Python.setup_install_args`在公式中描述的[公式作者的Python](Python-for-Formula-Authors.md).

### 升级MACOS

升级MACOS会导致如下错误:

-   `dyld: Library not loaded: /usr/local/opt/icu4c/lib/libicui18n.54.dylib`
-   `configure: error: Cannot find libz`

在MACOS升级之后,可能需要重新安装XCODE命令行工具和`brew upgrade`所有安装公式:

```sh
xcode-select --install
brew upgrade
```
