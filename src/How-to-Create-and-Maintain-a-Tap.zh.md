
# 如何创建和维护龙头

抽头是自制公式和/或外部命令的外部来源.它们可以由任何人创建,以向任何家庭用户提供自己的公式和/或外部命令.

## 创建龙头

tap通常是在线可用的Git存储库,但是您可以使用任何东西,只要它是Git理解的协议,或者甚至只是一个包含文件的目录.如果在GITHUB上托管,我们建议存储库的名称从`homebrew-`.

TAP公式遵循与内核的格式相同的格式,可以在存储库的根中添加,或在`Formula`或`HomebrewFormula`子目录.我们推荐后面的选项,因为它使存储库组织更容易掌握,并且顶级文件不与公式混合.

见[自制/核心](https://github.com/Homebrew/homebrew-core)对于一个水龙头的例子`Formula`子目录.

### 安装

如果它在GITHUB上,用户可以安装任何公式.`brew install user/repo/formula`. 自制将自动添加您的`github.com/user/homebrew-repo`在安装公式之前先敲击.`user/repo/formula`指向`github.com/user/homebrew-repo/**/formula.rb`文件在这里.

如果他们想要在不同时安装任何公式的情况下获得你的点击,用户可以将它添加到[`brew tap`命令](Taps.md).

如果是在GITHUB上,他们可以使用`brew tap user/repo`在哪里`user`是您的GITHUB用户名和`homebrew-repo`你的仓库.

如果它在GITHUB外部托管,就必须使用.`brew tap user/repo <URL>`在哪里`user`和`repo`将用来指你的水龙头和`<URL>`是你的Git克隆URL.

用户可以同时安装公式.`brew install foo`如果没有同名的核心公式,或`brew install user/repo/foo`避免冲突.

## 维修水龙头

一个TAP只是一个Git存储库,所以你不必做任何具体的修改,除了提交和推动你的变化.

### 更新

一旦安装了TAP,每次用户运行时,HOBBURW都会更新它.`brew update`. 过时的公式将在用户运行时升级.`brew upgrade`,就像核心公式一样.

## 外部命令

您可以为您的TAP用户提供自定义`brew`命令,将它们添加到`cmd`子目录.[多读外部命令](External-Commands.md).

见[自制/别名](https://github.com/Homebrew/homebrew-aliases)对于具有外部命令的TAP的示例.
