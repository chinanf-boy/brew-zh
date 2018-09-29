
# 新维护人员清单

**这是现有维护人员用来邀请新的维护者的指南.你可能会发现它很有趣,但这里没有什么用户需要知道的.**

有人长期为Homebrew做出高质量贡献,并且显示出自己能够做出比公式更新稍微高级一点的贡献?让我们邀请他们成为维护者吧!

首先,向他们发送邀请邮件:

```
The Homebrew team and I really appreciate your help on issues, pull requests and
your contributions to Homebrew.

We would like to invite you to have commit access and be a Homebrew maintainer.
If you agree to be a maintainer, you should spend a significant proportion of
the time you are working on Homebrew fixing user-reported issues, resolving any
issues that arise from your code in a timely fashion and reviewing user
contributions. You should also be making contributions to Homebrew every month
unless you are ill or on vacation (and please let another maintainer know if
that's the case so we're aware you won't be able to help while you are out).

You will need to watch Homebrew/brew and/or Homebrew/homebrew-core. Let us know
which (or both) so we can grant you commit access appropriately.

If you're no longer able to perform all of these tasks, please continue to
contribute to Homebrew, but we will ask you to step down as a maintainer.

A few requests:

- please make pull requests on any changes to Homebrew/brew code or any
  non-trivial (e.g. not a test or audit improvement or version bump) changes
  to formulae code and don't merge them unless you get at least one approval
  and passing tests.
- use `brew pull` for formulae changes that require new bottles or change
  multiple formulae and let it auto-close issues wherever possible (it may
  take ~5m). When this isn't necessary use GitHub's "Merge pull request"
  button in "create a merge commit" mode for Homebrew/brew or "squash and
  merge" for a single formulae change. If in doubt, check with e.g. GitX that
  you've not accidentally added merge commits
- still create your branches on your fork rather than in the main repository.
  Note GitHub's UI will create edits and reverts on the main repository if you
  make edits or click revert on the Homebrew/brew repository rather than your
  own fork.
- if still in doubt please ask for help and we'll help you out
- please read:
    - https://docs.brew.sh/Brew-Test-Bot-For-Core-Contributors
    - https://docs.brew.sh/Maintainer-Guidelines
    - anything else you haven't read on https://docs.brew.sh

How does that sound?

Thanks for all your work so far!
```

如果他们接受,遵循几个步骤让他们成立:

-   邀请他们到[**@自制/维护者**团队](https://github.com/orgs/Homebrew/teams/maintainers)(或任何相关)[子小组](https://github.com/orgs/Homebrew/teams/maintainers/teams)为他们提供对相关存储库的访问权限(但不要让它们成为所有者).他们将需要启用[GITHUB双因素认证](https://help.github.com/articles/about-two-factor-authentication/).
-   请他们签到[双托盘](https://bintray.com)使用他们的GITHUB帐户,他们应该自动同步到[宾托的家庭酿造组织](https://bintray.com/homebrew/organization/edit/members)作为会员,他们可以发布新的瓶子
-   将它们添加到[詹金斯的GITHUB授权设置管理用户名](https://jenkins.brew.sh/configureSecurity/)因此,他们可以调整设置和重新启动作业.
-   将它们添加到[詹金斯的GITHUB拉请求建设者管理列表](https://jenkins.brew.sh/configure)使能`@BrewTestBot test this please`为他们
-   邀请他们到[`homebrew-maintainers`私人维护者邮寄名单](https://lists.sfconservancy.org/mailman/admin/homebrew-maintainers/members/add)
-   邀请他们到[`machomebrew`私人维护者懈怠](https://machomebrew.slack.com/admin/invites)(并确保他们阅读了[通信指南](Maintainer-Guidelines.md#communication))
-   要求他们禁用SMS作为2FA设备,或者退回到GitHub帐户,支持使用其他认证方法之一.
-   要求他们定期复习删除不必要的东西[GITHUB个人访问令牌](https://github.com/settings/tokens)
-   将它们添加到[自制/酿造自述](https://github.com/Homebrew/brew/edit/master/README.md)

如果他们对系统管理工作感兴趣:

-   邀请他们到[`homebrew-ops`私人操作邮件列表](https://lists.sfconservancy.org/mailman/admin/homebrew-ops/members/add)
-   邀请他们到[`homebrew`私人密码](https://homebrew.1password.com/people)

如果他们想要消耗原始匿名聚合分析数据(而不是使用)`brew formula-analytics`):

-   邀请他们[谷歌分析](https://analytics.google.com/analytics/web/?authuser=1#management/Settings/a76679469w115400090p120682403/%3Fm.page%3DAccountUsers/)

一旦他们成为积极的维护者至少一年,并在一个以上的自制组织存储库(或一个存储库,并帮助系统管理工作)上进行了一些活动:

-   自酿啤酒[自由软件管理机构](https://sfconservancy.org)项目领导委员会可以就是否向维持者提供建议而加入委员会进行表决.如果他们接受了,把他们的名字、电子邮件和雇主发到HealBurW@ sFravaChan.Org,制作它们.[自酿GITHUB组织的所有者](https://github.com/orgs/Homebrew/people)并将它们添加到[自制/酿造自述](https://github.com/Homebrew/brew/edit/master/README.md).

如果有问题,请他们作为维护者下台,撤销他们对上述所有的访问.

现在坐下来,放松,让新的维护者处理更多的我们的贡献.
