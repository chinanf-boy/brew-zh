
# 匿名聚合用户行为分析

HealBurw已经开始收集匿名聚合用户行为分析,并将这些报告给谷歌Analytics.您将在第一次运行时通知您.`brew update`或者安装自制软件.

## 为什么?

自制饮料免费提供,在业余时间完全由志愿者操作.因此,我们没有资源对Homebrew用户进行详细的用户研究,以决定如何最好地设计未来的特性和优先考虑当前的工作.匿名聚合用户分析允许我们根据如何、何时何地和何时使用自制软件来优先定位修复和特征.例如:

-   如果一个公式被广泛使用并且经常失败,它将使我们能够优先考虑将公式固定在别人之上.
-   收集OS版本允许我们决定哪些版本的macOS优先次序并支持并确定只发生在单个版本上的构建失败.

## 多长时间?

HouBurw的匿名用户和事件数据有14个月的保留期.这就是[谷歌分析的最低可能值](https://support.google.com/analytics/answer/7667196).

## 什么?

HealBurw的分析记录了每个事件的一些共享信息:

-   家庭用户代理,例如`Homebrew/0.9.9 (Macintosh; Intel macOS 10.12.0) curl/7.43.0`
-   谷歌分析版,即`1`([http://开发商:谷歌.com/Analytics/DeValc/集合/协议/V1/参数ⅤV](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#v))
-   自制分析跟踪ID,例如`UA-75654628-1`([http://开发商:谷歌.com/Analytics/DeValc/集合/协议/V1/参数](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#tid))
-   自制分析用户ID,例如`1BAB65CC-FE7F-4D8C-AB45-B7DB5A6BA9CB`. 这是由`uuidgen`并存储在仓库特定的Git配置变量中`homebrew.analyticsuuid`在内部`$(brew --repository)/.git/config`. 这不允许我们跟踪单个用户,但能使我们准确地测量用户计数与事件计数.[http://开发商:谷歌.COM/Analytics/DeValc/集合/协议/V1/参数](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#cid))
-   如果启用了谷歌Analytics匿名IP设置,即`1`([http://开发商:谷歌.com/Analytics/DeValc/集合/协议/V1/参数](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#aip))
-   自制应用程序名称,例如`Homebrew`([http://开发商:谷歌.com/Analytics/DeVals/Studio/Value/V1/Type](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#an))
-   自制应用程序版本,例如`0.9.9`([http://开发商:谷歌.COM/Analytics/DeValc/集合/协议/V1/参数AVAV](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#av))
-   HouBurw分析击中类型,例如`event`([http://开发商:谷歌.COM/Analytics/DeVals/Copys/Value/V1/Type](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#t))

HoubBurw的分析记录了以下不同的事件:

-   安`event`命中类型`install`事件类别和来自非私有GITHUB TAP的HOBURW公式,以及任何使用的选项,例如`wget --with-pcre`作为动作和事件标签,例如`macOS 10.12, non-/usr/local, CI`指示操作系统版本,非标准安装位置和调用作为CI的一部分.这使我们能够识别需要固定的公式,并且在哪里更容易.
-   安`event`命中类型`install_on_request`事件类别和来自请求安装的非私有GitHub抽头的Homebrew公式(例如,使用`brew install`)加上选项和上面的事件标签.这使我们能够区分用户想要安装的公式和依赖的公式.
-   安`event`命中类型`cask_install`事件类别和来自非私有Github TAP的自制桶,作为上述操作和事件标签安装.这使我们能够识别需要固定的桶,更容易识别.
-   安`event`命中类型`BuildError`事件类别和无法安装的HOBBURW公式,例如`wget`作为动作和事件标签,例如`macOS 10.12`.

您还可以通过设置来查看由HealBurw的Analytics发送的所有信息.`HOMEBREW_ANALYTICS_DEBUG=1`在你的环境中.请注意,这也将停止任何分析被发送.

即使我们能够访问Homebrew分析用户ID(我们没有),Homebrew开发人员也不可能将任何特定事件匹配到任何特定用户.从谷歌Analytics中我们可以看到最用户特定的信息:

![Aggregate user analytics](assets/img/docs/analytics.png)

据我们所知,Google不可能将随机生成的纯自助分析用户ID与任何其他Google分析用户ID进行匹配.女装.

## 何时何地?

HutBurw的分析在整个家庭的执行过程中通过HTTPS发送到谷歌分析.

## 谁?

安装和错误分析的摘要是公开可用的[在这里](https://brew.sh/analytics/). JSON API也是可用的.

## 怎么用?

代码是可查看的[分析RB](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/utils/analytics.rb)和[分析学](https://github.com/Homebrew/brew/blob/master/Library/Homebrew/utils/analytics.sh). 它们是在单独的后台进程中完成的,并且失败很快,以避免延迟执行.如果你没有网络连接,他们会立即失败.

## 选择退出

自制分析帮助我们维护和离开它是值得赞赏的.但是,如果你想选择HouBurw的分析,你可以在你的环境中设置这个变量:

```sh
export HOMEBREW_NO_ANALYTICS=1
```

或者,这将防止分析被发送:

```sh
brew analytics off
```
