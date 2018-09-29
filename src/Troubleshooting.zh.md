
# 故障排除

**跑`brew update`两次`brew doctor` *之前*创造一个问题!**

此文档将帮助您检查常见问题,并确保您的问题尚未被报告.

## 检查常见问题

按照以下步骤解决常见问题:

-   跑`brew update`两次.
-   跑`brew doctor`修正所有的警告(**过时的XCODE/CLT和未经处理的DyLB很可能引起问题.**)
-   检查一下**XCODEL(CLT)的命令行工具**和**Xcode**是最新的.
-   如果命令在权限错误时失败,请检查权限`/usr/local`的子目录.如果你不确定该怎么办,你可以跑.`cd /usr/local && sudo chown -R $(whoami) bin etc include lib sbin share var opt Cellar Caskroom Frameworks`.
-   读完[常见问题](Common-Issues.md).

## 检查是否已报告问题

-   搜索[问题跟踪器](https://github.com/Homebrew/homebrew-core/issues)看看其他人是否已经报告过同样的问题.
-   确保在正确的存储库中搜索问题.如果一个失败的公式是非自制核心龙头的一部分,或者是一个桶的一部分.[自制/桶](https://github.com/Homebrew/homebrew-cask/issues)检查这些问题跟踪器.

## 创建问题

如果您的问题尚未解决或报告,那么创建一个问题:

0.  将调试信息上传到[主旨](https://gist.github.com):

-   如果你有一个公式相关的问题:运行`brew gist-logs <formula>`(何处)`<formula>`公式的名称.
-   如果遇到非公式问题:上载输出`brew config`和`brew doctor`新的[主旨](https://gist.github.com).

1.  [创造新的问题](https://github.com/Homebrew/homebrew-core/issues/new/choose).

-   给你的问题一个描述性的标题,包括公式名(如果适用)和你使用的MACOS版本.例如,如果一个公式无法建立,标题为您的问题"\\".<formula>未能在\\\\ 10 .x>上建立","<formula>"是无法构建的公式的名称,而'\\\< 10.x>"是您使用的MACOS的版本.
-   包含URL输出`brew gist-logs <formula>`(如适用).
-   包括指向您可能已经创建的任何附加GIST的链接(如输出的链接)`brew config`和`brew doctor`)
