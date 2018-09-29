
# 外部命令

自制,如Git,支持*外部命令*. 这使您可以创建新的命令,这些命令可以运行如下:

```sh
brew mycommand --option1 --option3 formula
```

不修改自制的内部设备.

## 命令类型

外部命令有两种味道:Ruby命令和shell脚本.

在这两种情况下,命令文件都应该是可执行的(`chmod +x`住在某处`PATH`.

### 红宝石命令

外部命令`extcmd`作为Ruby命令实现的应该命名为`brew-extcmd.rb`. 通过执行一个命令来执行命令.`require`在完全路径名上.因为命令是`require`d,它可以完全访问Homebrew"环境",即任何内部命令可以访问的所有全局变量和模块.小心使用自制的内部设备,它们随时可能发生变化而没有警告.

命令可以`Kernel.exit`如果需要状态代码,如果它没有明确退出,那么自制程序将返回.`0`.

### 外壳脚本

命令的shell脚本`extcmd`应该命名`brew-extcmd`. 此文件将通过`exec`将一些自制变量设置为环境变量,并传递任何附加命令行参数.

| 变量                      | 描述                                                                                 |
| ----------------------- | ---------------------------------------------------------------------------------- |
| `HOMEBREW_CACHE`        | 默认情况下,自制程序缓存下载TayBar到何处`~/Library/Caches/Homebrew`.                                |
| `HOMEBREW_CELLAR`       | 自酿窖的位置,软件在那里上演.这将是`HOMEBREW_PREFIX/Cellar`如果该目录存在,或`HOMEBREW_REPOSITORY/Cellar`否则. |
| `HOMEBREW_LIBRARY_PATH` | 包含自制程序应用程序代码的目录.                                                                   |
| `HOMEBREW_PREFIX`       | 其中自制软件安装软件.这一直是祖父母的目录`brew`可执行的,`/usr/local`默认情况下.                                 |
| `HOMEBREW_REPOSITORY`   | 如果从Git克隆中安装了存储库目录(即HealBurw的.git目录生存的地方).                                          |

请注意,脚本本身可以使用任何合适的SHBON(`#!`"行",因此可以为SH、BASH、Ruby或其他任何东西编写外部"shell脚本".

## 提供`--help`

所有内部和外部自制命令都可以提供样式.`--help`用线开始输出`#:`(然后评论)`:`在BASH和Ruby中的字符,然后输出`--help`.

例如,参见[页眉`brew services`](https://github.com/Homebrew/homebrew-services/blob/a5115e47b05e8d2a632ba7775599e698b240e5a2/cmd/brew-services.rb#L1-L31)输出`brew services --help`.

## 家庭自制组织外部命令

### 自酿活期支票

检查是否有一个新的上游版本的公式.见[`README`](https://github.com/Homebrew/homebrew-livecheck/blob/master/README.md)更多信息和用法.

安装使用:

```sh
brew tap homebrew/livecheck
```

### 找不到自制命令

乌本图`command-not-found equivalent`适合自制.见[`README`](https://github.com/Homebrew/homebrew-command-not-found/blob/master/README.md)更多信息和用法.

安装使用:

```sh
brew tap homebrew/command-not-found
```

### 家庭酿别名

允许您别名自制命令.见[`README`](https://github.com/Homebrew/homebrew-aliases/blob/master/README.md)更多信息和用法.

安装使用:

```sh
brew tap homebrew/aliases
```

## 非官方外部命令

这些命令由Homebrew用户提供,但不包括在主Homebrew组织中,也不由安装程序脚本安装.您可以手动安装它们,如上所述.

注意,它们基本上未被测试,并且总是在机器上运行未经测试的代码时要小心.

### 酿造宝石

安装任何`gem`包装成一个自给自足的自制酒窖位置:[HTTPS://GITHUBCOM/SPARTNTIG/BURW-GEM](https://github.com/sportngin/brew-gem)

注意这也可以安装在一起.`brew install brew-gem`.
