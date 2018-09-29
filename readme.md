# Homebrew/brew [![explain]][source] [![translate-svg]][translate-list] 
    
<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name
    

「 macOS 缺失的包管理器 」

[中文](./readme.md) | [english](https://github.com/Homebrew/brew) 


> jekyll 太慢了, 我用 mdbook:`md 输出 html`

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'Homebrew/brew' -->
<!-- commit = 'dae47914ca383e0ed5192436b9e7e11e0bf2640e' -->
<!-- time = '2018-09-27' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018-09-27 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/Homebrew/brew.svg
[commit]: https://github.com/Homebrew/brew/tree/dae47914ca383e0ed5192436b9e7e11e0bf2640e

<!-- doc-templite END generated -->


- [x] readme
- [ ] [docs](./src/readme.md)

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->


# 自酿啤酒-Homebrew

[![GitHub release](https://img.shields.io/github/release/Homebrew/brew.svg)](https://github.com/Homebrew/brew/releases)

特性、使用和安装说明都在[主页中概述](https://brew.sh). 术语(例如`地窖-Cellar`、`水龙头-Tap`、`木桶-Cask`等之间的区别)[在这里解释](https://docs.brew.sh/Formula-Cookbook#homebrew-terminology).

## 哪些软件包可用?

1.  输入`brew search`,输出一个列表.
2.  或参观[啤酒配方 formulae.brew.sh](https://formulae.brew.sh)在线浏览包.
3.  或使用`brew search --desc <关键词>`,命令行浏览包.

## 更多文档

`brew help`,`man brew`或检查[我们的文档](https://docs.brew.sh/).

## 故障排除

首先,请运行`brew update`和`brew doctor`.

第二,阅读[问题核对清单](https://docs.brew.sh/Troubleshooting).

**如果你不读这些,我们将花更长的时间来帮你解决问题.**

## 贡献

[![Travis](https://img.shields.io/travis/Homebrew/brew.svg)](https://travis-ci.org/Homebrew/brew)
[![Codecov](https://img.shields.io/codecov/c/github/Homebrew/brew.svg)](https://codecov.io/gh/Homebrew/brew)

我们希望你能为 Gomebrew 做贡献.首先,请阅读我们的[贡献指南](CONTRIBUTING.md)和[行为守则](CODE_OF_CONDUCT.md#code-of-conduct).

我们非常欢迎,从未贡献过开源的人的贡献: 我们都从初学者来的! 我们可以帮助建立一个部分工作的提交请求,目的是使之合并.我们也积极寻求使我们的贡献者多样化,特别欢迎来自所有背景和有色人种的妇女的贡献.

贡献的良好起点是运行`brew audit --strict`加上使用一些软件包(例如`brew audit --strict wget`,如果你使用`wget`) 然后阅读警告,尝试修复它们.直到`brew audit --strict`没有结果之后[提交拉动请求](https://docs.brew.sh/How-To-Open-a-Homebrew-Pull-Request). 如果您使用的`配方-formulae`没有警告，您可以在没有参数的情况下运行`brew audit --strict`，让它在所有包上运行并选择一个。

或者,对于更实质性的东西,请查看`help wanted`其中的一个问题.在[Homebrew/brew](https://github.com/homebrew/brew/issues?q=is%3Aopen+is%3Aissue+label%3A%22help+wanted%22)里面或[Homebrew/homebrew-core](https://github.com/homebrew/homebrew-core/issues?q=is%3Aopen+is%3Aissue+label%3A%22help+wanted%22).

祝你好运!

## 安全性

请向我们的[HackerOne](https://hackerone.com/homebrew/)报告安全问题.

## 你是谁?

Homebrew的主要领导者 [Mike McQuaid](https://github.com/mikemcquaid).

Homebrew 项目委员会 [Mike McQuaid](https://github.com/mikemcquaid), [JCount](https://github.com/jcount), [Misty De Meo](https://github.com/mistydemeo) and [Markus Reiter](https://github.com/reitermarkus).

Homebrew/brew 其他现有的维护者是 [Claudia](https://github.com/claui), [Michka Popoff](https://github.com/imichka), [Shaun Jackman](https://github.com/sjackman), [Chongyu Zhu](https://github.com/lembacon), [commitay](https://github.com/commitay), [Vitor Galvao](https://github.com/vitorgalvao), [JCount](https://github.com/jcount), [Misty De Meo](https://github.com/mistydemeo), [Gautham Goli](https://github.com/GauthamGoli), [Markus Reiter](https://github.com/reitermarkus), [Steven Peters](https://github.com/scpeters), [Jonathan Chang](https://github.com/jonchang) 和 [William Woodruff](https://github.com/woodruffw).

Homebrew/brew's Linux 支持 (和 Linuxbrew) 维护者 是 [Michka Popoff](https://github.com/imichka) 和 [Shaun Jackman](https://github.com/sjackman).

Homebrew/homebrew-core 的 其他当前维护者 [Claudia](https://github.com/claui), [Michka Popoff](https://github.com/imichka), [Shaun Jackman](https://github.com/sjackman), [Chongyu Zhu](https://github.com/lembacon), [commitay](https://github.com/commitay), [Izaak Beekman](https://github.com/zbeekman), [Sean Molenaar](https://github.com/SMillerDev), [Jan Viljanen](https://github.com/javian), [Viktor Szakats](https://github.com/vszakats), [FX Coudert](https://github.com/fxcoudert), [Steven Peters](https://github.com/scpeters), [JCount](https://github.com/jcount), [Misty De Meo](https://github.com/mistydemeo) and [Tom Schoonjans](https://github.com/tschoonj).

有重大贡献的前维护者包括 [Dominyk Tiller](https://github.com/DomT4), [Tim Smith](https://github.com/tdsmith), [Baptiste Fontaine](https://github.com/bfontaine), [Xu Cheng](https://github.com/xu-cheng), [Martin Afanasjew](https://github.com/UniqMartin),  [Brett Koonce](https://github.com/asparagui), [Charlie Sharpsteen](https://github.com/Sharpie), [Jack Nagel](https://github.com/jacknagel), [Adam Vandenberg](https://github.com/adamv), [Andrew Janke](https://github.com/apjanke), [Alex Dunn](https://github.com/dunn), [neutric](https://github.com/neutric), [Tomasz Pajor](https://github.com/nijikon), [Uladzislau Shablinski](https://github.com/vladshablinsky), [Alyssa Ross](https://github.com/alyssais), [ilovezfs](https://github.com/ilovezfs) 和 Homebrew 创建者: [Max Howell](https://github.com/mxcl).

## 社区

- [discourse.brew.sh (论坛)](https://discourse.brew.sh)
- [freenode.net\#machomebrew (IRC)](irc://irc.freenode.net/#machomebrew)
- [@MacHomebrew (Twitter)](https://twitter.com/MacHomebrew)

## 许可证

代码在[BSD 2条款"简化"许可证](LICENSE.txt). 文档是在[创作共享属性许可](https://creativecommons.org/licenses/by/4.0/).

## 捐赠

Homebrew是一个完全由无偿志愿者运营的非盈利性项目.我们需要您的资金来支付软件,硬件和主机围绕持续集成和项目的未来改进.每一笔捐款都将花在为我们的用户更好地制作Homebrew上.

请考虑通过Patreon定期捐款:

[![Donate with Patreon](https://img.shields.io/badge/patreon-donate-green.svg)](https://www.patreon.com/homebrew)

或者,如果你宁愿一次性付款:

-   [用PayPal捐款](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=V6ZE57MJRYC8L)
- Donate by USA $ check from a USA bank:
  - Make check payable to "Software Freedom Conservancy, Inc." and place "Directed donation: Homebrew" in the memo field.  Checks should then be mailed to:
    - Software Freedom Conservancy, Inc.
      137 Montague ST  STE 380
      BROOKLYN, NY 11201             USA
- Donate by wire transfer: contact accounting@sfconservancy.org for wire transfer details.

Homebrew is a member of the [Software Freedom Conservancy](https://sfconservancy.org) which provides us with an ability to receive tax-deductible, Homebrew earmarked donations (and [many other services](https://sfconservancy.org/members/services/)). Software Freedom Conservancy, `Inc. is a 501(c)(3)` organization incorporated in New York, and donations made to it are fully tax-deductible to the extent permitted by law.

## 赞助商

Our Xserve ESXi boxes for CI are hosted by [MacStadium](https://www.macstadium.com).

[![Powered by MacStadium](https://cloud.githubusercontent.com/assets/125011/22776032/097557ac-eea6-11e6-8ba8-eff22dfd58f1.png)](https://www.macstadium.com)

Our Jenkins CI installation is hosted by [DigitalOcean](https://m.do.co/c/7e39c35d5581).

![DigitalOcean](https://cloud.githubusercontent.com/assets/125011/26827038/4b7b5ade-4ab3-11e7-811b-fed3ab0e934d.png)

Our physical hardware is hosted by [Commsworld](https://www.commsworld.com).

![Commsworld powered by Fluency](https://user-images.githubusercontent.com/125011/30822845-1716bc2c-a222-11e7-843e-ea7c7b6a1503.png)

Our bottles (binary packages) are hosted by [Bintray](https://bintray.com/homebrew).

[![Downloads by Bintray](https://bintray.com/docs/images/downloads_by_bintray_96.png)](https://bintray.com/homebrew)

Secure password storage and syncing provided by [1Password for Teams](https://1password.com/teams/) by [AgileBits](https://agilebits.com).

[![AgileBits](https://da36klfizjv29.cloudfront.net/assets/branding/agilebits-fcca96e9b8e815c5c48c6b3e98156cb5.png)](https://agilebits.com)

Homebrew is a member of the [Software Freedom Conservancy](https://sfconservancy.org).

[![Software Freedom Conservancy](https://sfconservancy.org/img/conservancy_64x64.png)](https://sfconservancy.org)
