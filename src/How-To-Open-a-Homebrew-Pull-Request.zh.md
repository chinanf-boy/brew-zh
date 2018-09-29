
# 如何打开自制中断请求(并将其合并)

Homebrew贡献者使用以下命令在GitHub上设置Homebrew的Git存储库的分支,创建新的分支并创建该分支中的更改的GitHub拉请求("PR").

根据您想要进行的更改,需要将拉请求发送到Homebrew的主存储库中的适当一个存储库.如果你想提交一个改变自制代码的核心代码`brew`实现),您应该打开拉请求[自制/酿造](https://github.com/Homebrew/brew). 如果您想提交一个公式的更改,您应该打开[这个`homebrew/core`水龙头](https://github.com/Homebrew/homebrew-core)或另一个[官方抽头](https://github.com/Homebrew),根据公式类型.

## 提交现有公式的新版本

1.  使用`brew bump-formula-pr`用一个命令来做任何事情(即分叉、提交、推送).跑`brew bump-formula-pr --help`学习更多.

## 建立自己的自制软件仓库

### 核心`brew`代码相关的拉动请求

1.  [在Github上移植自制/酿造仓库](https://github.com/Homebrew/brew/fork).

-   这将创建一个可以推到的个人远程存储库.这是需要的,因为只有自制软件维护者才有权进入主要的存储库.

2.  更改包含您的自制程序的目录`cd $(brew --repository)`.
3.  添加你的可推叉仓库`git remote add <YOUR_USERNAME> https://github.com/<YOUR_USERNAME>/brew.git`.

-   `<YOUR_USERNAME>`是您的GITHUB用户名,不是本地机器用户名.

### 有关拉动请求的公式

1.  [在Github上移植自制/自制的核心存储库](https://github.com/Homebrew/homebrew-core/fork).

-   这将创建一个可以推到的个人远程存储库.这是需要的,因为只有自制软件维护者才有权进入主要的存储库.

2.  更改包含自制公式的目录`cd $(brew --repository homebrew/core)`.
3.  添加你的可推叉仓库`git remote add <YOUR_USERNAME> https://github.com/<YOUR_USERNAME>/homebrew-core.git`

-   `<YOUR_USERNAME>`是您的GITHUB用户名,不是本地机器用户名.

## 从新分支创建您的拉请求

要创建一个新的分支并提交它进行审查,请创建一个GITHUB拉请求,其步骤如下:

1.  退房`master`分支机构`git checkout master`.
2.  检索新的更改`master`分支机构`brew update`.
3.  从最新创建一个新的分支`master`分支机构`git checkout -b <YOUR_BRANCH_NAME> origin/master`.
4.  做出改变.对于公式,使用`brew edit`或者你最喜欢的文本编辑器,遵循所有的指南[公式食谱](Formula-Cookbook.md).

-   如果有`bottle do`方块中的公式,不要删除或更改它;我们会更新它时,我们拉你的PR.

5.  通过执行以下测试来测试更改,并确保它们无问题地通过.对于变化的公式,请务必做.`brew audit`在安装更改公式时执行步骤.

-   `brew tests`
-   `brew install --build-from-source <CHANGED_FORMULA>`
-   `brew test <CHANGED_FORMULA>`
-   `brew audit --strict <CHANGED_FORMULA>`

6.  对每一个改变的公式做出单独的提交`git add`和`git commit`.
7.  把你的新约定上传到你的叉子上`git push --set-upstream <YOUR_USERNAME> <YOUR_BRANCH_NAME>`.
8.  转到相关的存储库(例如[HTTPS://GITHUBCOM/HOMEBWW/BRW](https://github.com/Homebrew/brew),[HTTPS://GITHUBCOM/HOMEBWW/HOMEBRW-CORE](https://github.com/Homebrew/homebrew-core)等,并创建一个拉请求,要求审查和合并的提交在您的推动分支.解释为什么需要改变,如果修复bug,如何重现bug.确保你已经完成了在你的新PR中出现的清单中的每一步.

-   请注意,我们对于简单版本更新的首选提交消息格式是"`<FORMULA_NAME> <NEW_VERSION>`"例如"`source-highlight 3.1.8`".`devel`版本更新应该具有提交消息.`(devel)`,例如"`nginx 1.9.1 (devel)`".如果同时更新`stable`和`devel`格式应该是这两种形式的连接,例如"`x264 r2699, r2705 (devel)`".

9.  等待反馈或来自自制软件的维护者的合并.我们通常在几天内响应所有PRS,但可能需要长达一个星期,这取决于维护人员的工作量.

谢谢您!

## 跟进

对反馈作出良好反应:

1.  要求澄清任何你不理解的事情,并帮助你做任何你不知道该怎么做的事情.
2.  你贴上拉要求评论,如果你提供的所有变更请求的信息,它没有被合并后的一个星期.如果你陷入困境需要帮助,就发表评论.

-   一`needs response`PR上的标签意味着自制软件维护者需要你对先前的评论做出回应.

3.  除非有其他要求,否则请在拉取请求中保持讨论(即不要私下向维护者发电子邮件).
4.  不要在关闭的拉请求中继续讨论.
5.  不要和自制软件维护者争论.你可能不同意,但除非他们改变主意,请执行他们的要求.最终,他们控制了在自制中所包含的内容,因为它们必须支持所做的任何更改.

基于反馈进行更改:

1.  再次检查你的分支`git checkout <YOUR_BRANCH_NAME>`.
2.  进行任何请求的更改并提交`git add`和`git commit`.
3.  SpCub新提交到每个公式的一个提交`git rebase --interactive origin/master`.
4.  推到远程叉的分支和拉请求`git push --force`.

如果你正在做一个单一公式的PR,`git commit --amend`当你走的时候,是一个很方便的方法.

一旦所有的反馈都被解决了,如果它是我们想要包含的更改(包括大多数更改),那么我们将把您的提交添加到Homebrew.请注意,由于我们合并捐款的方式,PR状态可能显示为"关闭"而不是"合并".不要担心:在实际合并提交中,您仍然可以获得作者信用.

做得好,你现在是一个自制啤酒的贡献者!
