
# 抽头(第三方储存库)

`brew tap`将更多的存储库添加到公式列表中`brew`跟踪、更新和安装.默认情况下,`tap`假设存储库来自GITHUB,但命令不限于任何一个位置.

## 命令(`brew tap`)

-   `brew tap`没有参数列出当前挖掘的存储库.例如:

```sh
$ brew tap
homebrew/core
mistydemeo/tigerbrew
dunn/emacs
```

-   `brew tap <user/repo>`对仓库进行浅层克隆.[HTTPS://Github. COM/USER/RIPO](https://github.com/user/repo). 之后,`brew`将能够在这些公式中工作,就像它们在自制的标准知识库中一样.您可以安装和卸载它们.`brew [un]install`,当运行时,公式会自动更新.`brew update`. (详情见下文)`brew tap`处理存储库的名称.

-   `brew tap <user/repo> <URL>`对URL库进行浅层克隆.与一个参数版本不同,URL不被假定为GITHUB,并且它不必是HTTP.GIT可以处理的任何位置和任何协议都很好.

-   添加`--full`对于上面的一个或两个参数调用,Git将是一个完整的克隆而不是一个浅的克隆.完整是默认的自制程序开发者.

-   `brew tap --repair`从基于目录结构的SyLink迁移抽取公式.(这应该只需要运行一次.)

-   `brew untap user/repo [user/repo user/repo ...]`移除给定的抽头.存储库被删除,`brew`将不再知道他们的公式.`brew untap`可以同时处理多次删除.

## 知识库命名约定和假设

-   在GITHUB上,您的存储库必须命名.`homebrew-something`为了使用一个参数形式`brew tap`.  前缀"自制"不是可选的.(这两个参数表单没有这个限制,但它迫使您显式地给出完整URL.)

-   当你使用`brew tap`但是,在命令行中,您可以省略命令中的"自制程序"前缀.

    也就是说,`brew tap username/foobar`可以用作长版本的捷径:`brew tap username/homebrew-foobar`. `brew`每当必要时,它会自动添加"自制程序"前缀.

## 公式重复名称

如果您的水龙头包含一个公式,也存在于[`homebrew/core`](https://github.com/Homebrew/homebrew-core)这很好,但是它意味着你必须默认地显式安装它.

如果你想优先考虑轻敲`homebrew/core`,你可以使用`brew tap-pin username/repo`钉龙头,并使用`brew tap-unpin username/repo`恢复引脚.

无论何时`brew install foo`发出命令,`brew`将按以下顺序查找要使用的公式:

-   固定丝锥
-   核心公式
-   其他抽头

如果需要从特定的筛选器安装公式,可以使用完全限定的名称来引用它们.

例如,您可以为替代创建一个TAP.`vim`公式.如果不钉住它,它的行为将是

```sh
brew install vim                     # installs from homebrew/core
brew install username/repo/vim       # installs from your custom repo
```

但是如果你把水龙头钉上`brew tap-pin username/repo`您将需要使用`homebrew/core`参考核心公式.

```sh
brew install vim                     # installs from your custom repo
brew install homebrew/core/vim       # installs from homebrew/core
```

请注意,只有当公式名称由您直接给出时,才对固定抽头进行优先级排序,也就是说,它不会影响作为依赖项自动安装的公式.
