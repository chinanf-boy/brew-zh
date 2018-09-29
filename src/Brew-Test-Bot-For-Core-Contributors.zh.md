
# BREW测试BOT为核心贡献者

如果生成已运行并通过`brew test-bot`然后,它可以用来快速瓶公式.

有两种类型的詹金斯作业将与之交互:

## [自制核心拉动请求](https://jenkins.brew.sh/job/Homebrew%20Core/)

这项工作自动构建任何提交请求到自制/自制软件的核心.在成功或失败时,它更新拉请求状态(参见[主酿测试BOT文档页](Brew-Test-Bot.md))在成功构建时,它自动上载瓶子.

## [自制测试](https://jenkins.brew.sh/job/Homebrew%20Testing/)

此作业手动触发运行.[`brew test-bot`](https://github.com/Homebrew/homebrew-test-bot/blob/master/cmd/brew-test-bot.rb)使用用户指定的参数.在成功构建时,它自动上载瓶子.

您可以手动启动具有参数运行的作业.[`brew test-bot`](https://github.com/Homebrew/homebrew-test-bot/blob/master/cmd/brew-test-bot.rb)具有相同的参数.通过pull请求URL、commit URL、commit SHA-1和/或公式名称让Brew Test Bot测试它们、报告结果并生产瓶子通常是有用的.

## 装瓶

拉动和装瓶拉动请求`brew pull`:

1.  确保工作顺利完成.
2.  跑`brew pull --bottle 12345`哪里`12345`是拉请求号(或URL).如果它抱怨一个丢失的URL`BrewTestBot`然后,瓶子还没有完成上传,等待并稍后再试.
3.  跑`git push`推动提交.

设置测试生成:

1.  确保工作顺利完成.
2.  跑`brew pull --bottle https://jenkins.brew.sh/job/Homebrew%20Testing/1234/`哪里`https://jenkins.brew.sh/job/Homebrew%20Testing/1234/`是詹金斯中的测试生成URL.
3.  跑`git push`推动提交.
