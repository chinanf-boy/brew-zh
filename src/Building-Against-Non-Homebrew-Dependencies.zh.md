
# 建立非自制依赖关系

## 历史

最初,Homebrew是一个从源构建的包管理器,所有用户环境变量和非Homebrew安装的软件都可用于构建.从那时起,自制啤酒增加了`Requirement`s指定非自制软件的依赖性(如由`brew cask`像x11/x石英一样,`superenv`构建系统以去除未指定的依赖项,环境过滤以阻止用户环境泄漏到Homebrew构建,以及`default_formula`指定一个`Requirement`可以用一个特定的公式来满足.

由于自制软件主要是二进制包管理器,大多数用户都在满足.`Requirement`S与`default_formula`不是随意选择.为了改进质量和减少变化,Homebrew现在只支持使用默认公式,作为普通的依赖项,而不再支持使用任意的替代项.

## 今天

如果您希望构建由自制程序提供的自定义非自制软件依赖项(例如非自制程序、非MACOS)`ruby`那么你必须[创建和维护您自己的水龙头](How-to-Create-and-Maintain-a-Tap.md)由于这些公式将不被接受在自制/自制核心.一旦你做到了,你就可以指定`env :std`在公式中允许`which ruby`访问现有的`PATH`变量,并允许编译与此红宝石链接.
