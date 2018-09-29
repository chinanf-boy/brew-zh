
# 酿造试验机器人

`brew test-bot`是自动审查和测试系统的名称[我们的Kickstarter在2013](https://www.kickstarter.com/projects/homebrew/brew-test-bot).

它包括四个Mac Mini和三个XServer,它们在两个数据中心运行.[詹金斯实例在HTTPS://Junk.BurW.SH](https://jenkins.brew.sh)然后运行[`brew-test-bot.rb`](https://github.com/Homebrew/homebrew-test-bot/blob/master/cmd/brew-test-bot.rb)Ruby脚本,用于执行提交到主分支、拉请求和维护人员请求的自定义构建的自动测试.

## 拉动请求

BOT自动建立拉请求并根据作业的结果更新它们的状态.

例如,已经排队但尚未完成的作业将在拉请求中有一个这样的部分:

![Triggered Pull Request](assets/img/docs/brew-test-bot-triggered-pr.png)

* * *

失败的构建看起来像这样:

![Failed Pull Request](assets/img/docs/brew-test-bot-failed-pr.png)

* * *

经过的构建看起来像这样:

![Passed Pull Request](assets/img/docs/brew-test-bot-passed-pr.png)

* * *

在失败或通过的构建中,您可以单击"详细信息"链接来查看詹金斯中的结果.

经过的构建看起来像这样:

![Passed Jenkins Build](assets/img/docs/brew-test-bot-passed-jenkins.png)

* * *

失败的构建看起来像这样:

![Failed Jenkins Build](assets/img/docs/brew-test-bot-failed-jenkins.png)

* * *

您可以单击测试结果链接(例如`brew-test-bot.el_capitan.install openssl`)查看失败的测试输出:

![Failed Test](assets/img/docs/brew-test-bot-failed-test.png)

* * *
