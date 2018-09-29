
# BREW(1)——MACOS的丢失包管理器

## 简介

`brew` `--version`<br>
`brew` `command` [`--verbose`γ`-v`][`options`] [`formula`]…

## 描述

HOMBURW是最简单最灵活的安装苹果未包含MaCMOS的UNIX工具的方法.

## 基本命令

有关完整命令列表,请参见[命令](#commands)部分.

用`--verbose`或`-v`许多命令打印额外的调试信息.注意,这些标志应该只出现在命令之后.

-   `install` `formula`安装`formula`.

-   `uninstall` `formula`卸载`formula`.

-   `update`从Github中获取最新版本的自制程序`git`(1).

-   `list`列出所有已安装的公式.

-   `search`(`text`γ```/``text``/```):执行公式名称的子字符串搜索`text`. 如果`text`被斜杠包围,然后被解释为正则表达式.寻找`text`在线推广到一些流行的抽头.如果不给出搜索项,则列出所有局部可用公式.

## 命令

-   `analytics` [`state`]显示匿名用户行为分析状态.更多阅读[HTTPS://DOCS.BURW.SH/分析](https://docs.brew.sh/Analytics).

-   `analytics`(`on`γ`off`打开/关闭HouBurw的分析.

-   `analytics` `regenerate-uuid`再生UUID用于家庭分析.

-   `cat` `formula`显示源到`formula`.

-   `cleanup` [```--prune=``days```][`--dry-run`] [`-s`][<formula/cask> ...]删除过时的锁文件和公式和桶的过期下载,并删除已安装公式的旧版本.如果指定了参数,则只针对指定的公式和桶进行此操作.

    如果```--prune=``days```指定,删除所有缓存文件`days`.

    如果`--dry-run`或`-n`通过,显示什么将被删除,但实际上没有删除任何东西.

    如果`-s`通过,擦除缓存,包括下载,即使是最新版本.注:任何安装的公式或木桶的下载都不会被删除.如果你也想删除那些:`rm -rf "$(brew --cache)"`

-   `command` `cmd`显示调用时使用的文件的路径`brew` `cmd`.

-   `commands` \[`--quiet` [`--include-aliases`]显示内置和外部命令的列表.

    如果`--quiet`通过,只列出没有标题的命令的名称.用`--include-aliases`内部命令的别名将被包括在内.

-   `config`显示用于调试的自制程序和系统配置.如果你提交了一个bug报告,如果你不提供它,你很可能会被要求得到这个信息.

-   `deps` [`--1`][`-n`] [`--union`][`--full-name`] [`--installed`][`--include-build`] [`--include-optional`][`--skip-recommended`] [`--include-requirements`] `formulae`显示依赖关系`formulae`. 当给定多个公式参数时,显示依赖关系的交集.`formulae`.

    如果`--1`通过,只显示一个级别的依赖项,而不是递归.

    如果`-n`传递,以拓扑顺序显示依赖项.

    如果`--union`通过,显示依赖的联合`formulae`而不是十字路口.

    如果`--full-name`通过它们的全名传递列表依赖项.

    如果`--installed`通过,只列出当前安装的依赖项.

    默认情况下,`deps`显示所需和推荐的依赖关系`formulae`. 包括`:build`类型依赖性`--include-build`. 同样,通过`--include-optional`包括`:optional`依赖关系或`--include-test`包括(非递归)`:test`依赖关系.跳过`:recommended`类型依赖性`--skip-recommended`. 除了依赖项之外还包括要求`--include-requirements`.

-   `deps` `--tree` [`--1`][`filters`] [`--annotate`](`formulae`|`--installed`)将依赖项显示为树.当给定多个公式参数时,为每个公式输出单个树.

    如果`--1`通过,只显示一个级别的儿童.

    如果`--installed`通过,为每个已安装的公式输出一棵树.

    这个`filters`占位符是选项的任意组合.`--include-build`,`--include-optional`,`--include-test`,`--skip-recommended`和`--include-requirements`如上所述.

    如果`--annotate`通过,生成、可选和推荐的依赖项在输出中被标记为这样.

-   `deps` [`filters`](`--installed`|`--all`):显示已安装或所有可用公式的依赖项.每一行输出都从公式名开始,后面跟着冒号和该公式的所有直接依赖关系.

    这个`filters`占位符是选项的任意组合.`--include-build`,`--include-optional`,`--include-test`和`--skip-recommended`如上所述.

-   `desc` `formula`显示`formula`的名字和一行描述.

-   `desc` [`--search`γ`--name`γ`--description`](`text`|`/``text``/`)搜索名字和描述(`--search`或`-s`的名称,(就)`--name`或`-n`的描述(或生产)`--description`或`-d`)`text`.......如果`text`它是由slashes flanked,interpreted表达的调节.公式描述的高速缓存是由缓存;在网上搜索,使搜索subsequent比这慢........

-   `diy` [```--name=``name```][`--version=``version`]自动确定的前缀是:非安装自制软件.

    使用输出从命令,你可以安装你自己的软件,然后连接到衣领这与自制的前缀`brew link`.......

    该选项```--name=``name```和```--version=``version```每个带一个参数的设置和允许你明确的名称和版本,你installing封装.

-   `doctor`检查您的系统:潜在的问题.医生与非零退出状态是发现潜在的问题(如有).请注意,这些警告都只是用来帮助调试运行与维护的一个问题,如果你的文件.如果你正在使用的自制是一切美术:请放心或文件只是忽略这一问题;.......

-   `fetch` [`--force`][`--retry`] [`-v`][`--devel`|`--head`] [`--deps`][`--build-from-source`|`--force-bottle`] `formulae`下载给定的源包`formulae`. 对于TARBOARS,还打印SHA256校验和.

    如果`--HEAD`或`--devel`通过,获取该版本而不是稳定版本.

    如果`-v`通过,做一个详细的VCS结账,如果URL代表一个VCS.这对于查看现有的VCS缓存是否已经更新是有用的.

    如果`--force`(或)`-f`通过,删除以前缓存的版本和重新获取.

    如果`--retry`通过,如果下载失败或重新下载,如果先前缓存的版本的校验和不再匹配,则重试.

    如果`--deps`通过,也可以下载任何列表中的依赖项`formulae`.

    如果`--build-from-source`(或)`-s`通过,下载源而不是瓶子.

    如果`--force-bottle`通过,如果为当前或最新版本的macOS存在瓶子,则下载该瓶子,即使该瓶子在安装期间不使用.

-   `gist-logs` [`--new-issue`|`-γ`n] `formula`为失败的构建文件上传日志`formula`一个新的要点.

    `formula`通常是要安装的公式的名称,但是它可以用几种不同的方式来指定.见[指定公式](#specifying-formulae).

    如果`--with-hostname`通过,包括主旨中的主机名.

    如果`--new-issue`通过,在适当的GITHUB存储库中自动创建一个新的问题,并创建要点.

    如果未找到日志,则会出现错误消息.

-   `home`在浏览器中打开自己的主页.

-   `home` `formula`打开`formula`在浏览器中的主页.

-   `info`为您的自制产品安装简要统计.

-   `info` `formula`(`--verbose`):显示有关`formula`和分析数据(既不提供)`HOMEBREW_NO_ANALYTICS`或`HOMEBREW_NO_GITHUB_API`设置)

    通过`--verbose`查看更详细的分析数据.

-   `info` `--github` `formula`打开一个浏览器到GITHUB历史页面`formula`.

    在本地查看公式历史:`brew log -p`公式

-   `info` ```--json=``version```(`--all`γ`--installed`γ`formulae`):打印一个JSON表示`formulae`. 目前唯一接受的价值`version`是`v1`.

    通过`--all`获取所有公式的信息,或`--installed`获取所有安装公式的信息.

    有关使用JSON输出的示例,请参阅文档:[HTTPS://DOCS.BURW.S/QueReIn Burw](https://docs.brew.sh/Querying-Brew)

-   `install` [`--debug`][`--env=`(`std`|`super`)] [`--ignore-dependencies`γ`--only-dependencies`][`--cc=``compiler`] [`--build-from-source`γ`--force-bottle`][`--include-test`] [`--devel`γ`--HEAD`][`--keep-tmp`] [`--build-bottle`][`--force`] [`--verbose`][`--display-times`] `formula` [`options`…...]安装`formula`.

    `formula`通常是要安装的公式的名称,但是它可以用几种不同的方式来指定.见[指定公式](#specifying-formulae).

    如果`--debug`(或)`-d`传递并酿造失败,打开具有对IRB或临时构建目录内的shell的访问的交互式调试会话.

    如果`--env=std`通过,使用标准生成环境而不是SufEnv.

    如果`--env=super`传递,使用SufEnv,即使公式指定标准生成环境.

    如果`--ignore-dependencies`通过,跳过安装任何类型的依赖项.如果它们还不存在,则公式可能无法安装.

    如果`--only-dependencies`通过指定的选项安装依赖项,但不要安装指定的公式.

    如果```--cc=``compiler```通过,尝试编译使用`compiler`. `compiler`应该是编译器的可执行文件的名称,例如`gcc-8`对于GCC 8,`gcc-4.2`对于苹果的GCC 4.2,或`gcc-4.9`提供GCC 4.9的自制程序.为了使用LLVM的铿锵,使用`llvm_clang`. 若要指定苹果提供的CLAN,请使用`clang`. 此参数只接受由自制程序或与MACOS捆绑提供的编译器.在使用此标志时,如果遇到错误,请不要提交文件.

    如果`--build-from-source`(或)`-s`通过,编译指定的`formula`从源头上,即使提供了一个瓶子.依赖性仍然将被安装从瓶子,如果他们是可用的.

    如果`HOMEBREW_BUILD_FROM_SOURCE`被设置,不管是否`--build-from-source`通过,然后两者`formula`而且,作为瓶子的一部分安装的依赖项是从源建立的,即使瓶子是可用的.

    如果`--force-bottle`如果是当前版本或最新版本的macOS,即使它通常不会用于安装,也可以通过瓶子进行安装.

    如果`--include-test`通过,安装测试依赖关系.这些只需要公式维护人员运行.`brew test`.

    如果`--devel`通过,以及`formula`定义它,安装开发版本.

    如果`--HEAD`通过,以及`formula`定义它,安装头版本,主,躯干,不稳定.

    如果`--keep-tmp`通过,安装过程中创建的临时文件不会被删除.

    如果`--build-bottle`通过,准备在安装过程中最终装瓶的配方.

    如果`--force`(或)`-f`通过,不必检查以前安装的KEG版本或非迁移版本

    如果`--verbose`(或)`-v`通过,打印验证和安装后的步骤.

    如果`--display-times`通过,在运行结束时打印每个公式的安装时间.

    特定安装选项`formula`可以附加到命令中,并且可以列出`brew options` `formula`.

-   `install` `--interactive` [`--git`] `formula`如果`--interactive`(或)`-i`通过、下载和修补`formula`然后打开一个外壳.这允许用户运行.`./configure --help`否则就决定如何将软件包转换成自制公式.

    如果`--git`(或)`-g`通过,自制程序将创建一个Git存储库,用于为软件创建补丁.

-   `leaves`:显示已安装的公式,而不是另一个已安装公式的依赖关系.

-   `ln`,`link` [`--overwrite`][`--dry-run`] [`--force`] `formula`SyLink全部`formula`将安装的文件放入自制程序前缀.这在安装公式时是自动完成的,但对于DIY安装是有用的.

    如果`--overwrite`通过,HOBPROW将删除在链接中已经存在的前缀文件.

    如果`--dry-run`或`-n`通过,自制程序将列出所有链接或删除的文件.`brew link --overwrite`,但实际上不会链接或删除任何文件.

    如果`--force`(或)`-f`通过,自制程序只允许KEG公式链接.

-   `list`,`ls` [`--full-name`][`-1`] [`-l`][`-t`] [`-r`]列出所有已安装的公式.如果`--full-name`通过,打印公式完全限定名称.如果`--full-name`没有通过,其他选项(即`-1`,`-l`,`-t`和`-r`)传递给`ls`产生实际输出.

-   `list`,`ls` `--unbrewed`列出未通过自制程序安装的自制文件前缀中的所有文件.

-   `list`,`ls` [`--verbose`]`--versions` [`--multiple`]] [`--pinned`][`formulae`]列出已安装的文件`formulae`. 结合`--verbose`递归地列出每个子目录的内容`formula`小桶.

    如果`--versions`通过,显示已安装公式的版本号,或仅指定公式`formulae`给出.用`--multiple`只显示具有多个版本的公式.

    如果`--pinned`通过,显示钉住公式的版本,或者只有指定的(钉住)公式`formulae`给出.也见`pin`,`unpin`.

-   `log` [`git-log-options`] `formula`……:显示给定公式的Git日志.选项`git-log`(1)识别可以在公式列表之前通过.

-   `migrate` [`--force`] `formulae`:将重命名包迁移到新名称,在哪里`formulae`是包的旧名称.

    如果`--force`(或)`-f`)通过,然后处理安装`formulae`并通过`formulae`就像他们来自同一个水龙头并迁移他们一样.

-   `missing` [```--hide=``hidden```][`formulae`]检查给定的`formulae`缺少依赖项.如果没有`formulae`给出,检查所有安装的啤酒.

    如果```--hide=``hidden```通过,仿佛没有`hidden`安装完毕.`hidden`应该是一个逗号分隔的公式列表.

    `missing`如果任何公式缺少依赖关系,则退出具有非零状态.

-   `options` [`--compact`](`--all`|`--installed`|`formulae`)显示特定安装选项`formulae`.

    如果`--compact`通过一个由空格分隔的单行显示所有选项.

    如果`--all`通过,显示所有公式的选项.

    如果`--installed`通过,显示所有已安装公式的选项.

-   `outdated` [`--quiet`γ`--verbose`γ```--json=``version```][`--fetch-head`]显示具有更新版本的公式.

    默认情况下,在交互shell中显示版本信息,否则将被抑制.

    如果`--quiet`通过,只列出过时酿造品的名称(优先)`--verbose`)

    如果`--verbose`(或)`-v`通过,显示详细的版本信息.

    如果```--json=``version```通过,输出将以JSON格式.目前唯一接受的价值`version`是`v1`.

    如果`--fetch-HEAD`通过,获取上游存储库,以检测该公式的头安装是否过时.否则,当新的稳定版本或发布版本被释放时,将检查存储库的头部是否更新.

-   `pin` `formulae`引脚指定`formulae`防止发行时升级`brew upgrade`公式命令.也见`unpin`.

-   `postinstall` `formula`重新安装后安装步骤`formula`.

-   `prune` [`--dry-run`]从HOBPROW前缀删除死链接.这通常是不需要的,但在进行DIY安装时可能有用.

    如果`--dry-run`或`-n`通过,显示什么将被删除,但实际上没有删除任何东西.

-   `readall` [`--aliases`][`--syntax`] [`taps`]导入指定的所有公式`taps`(默认为所有安装的抽头).

    这对于调试所有公式时进行重大更改非常有用.`formula.rb`测试加载所有公式的性能,或者确定当前公式是否有红宝石问题.

    如果`--aliases`通过,也验证每个别名在每个抽头中的链接.

    如果`--syntax`通过,也语法检查所有的自制的Ruby文件.

-   `reinstall` [`--display-times`] `formula`卸载然后安装`formula`(使用现有安装选项).

    如果`--display-times`通过,在运行结束时打印每个公式的安装时间.

-   `search`,`-S`显示所有局部可用公式(包括抽头公式).没有进行在线搜索.

-   `search` `--casks`显示所有本地可用的桶(包括轻敲的).没有进行在线搜索.

-   `search` [`--desc`](`text`|`/``text``/`)执行对容器符号和公式名称的子字符串搜索.`text`. 如果`text`被斜杠包围,然后被解释为正则表达式.寻找`text`扩展到官方抽头.

    如果`--desc`传递,搜索公式与描述匹配`text`有名字匹配的桶`text`.

-   `search`(`--debian`γ`--fedora`γ`--fink`γ`--macports`γ`--opensuse`γ`--ubuntu`)`text`寻找`text`在给定的包管理器列表中.

-   `sh` [`--env=std`]启动一个自制的构建环境外壳.使用我们多年来的精悍自制软件来帮助你`./configure && make && make install`甚至你的`gem install`成功.特别是如果你只在XCODE配置下运行自制程序,因为它添加了类似的工具.`make`对你`PATH`否则构建系统将找不到.

    如果`--env=std`通过,使用标准`PATH`而不是SufEnv公司的.

-   `shellenv`打印导出语句——在shell中运行它们,Homebrew的安装将包括在PATH、MANPATH和INFOPATH中.

    HOMBRWWYPROFIX、HOBBRWYM窖和HOMBRWWORKPOLD也被导出以保存这些变量的多个查询.

    考虑在DOTFACK中添加输出的评估(例如).`~/.profile`用`eval $(brew shellenv)`

-   `style` [`--fix`][`--display-cop-names`] [```--only-cops=``cops```γ```--except-cops=``cops```][`files`|`taps`|`formulae`]检查公式或文件是否符合自制风格指南.

    清单`files`,`taps`和`formulae`可能无法组合.如果没有提供,`style`将对整个自制库进行风格检查,包括核心代码和所有公式.

    如果`--fix`通过RuBOCOP的自动纠正功能自动修复样式违反.

    如果`--display-cop-names`通过,在输出中包含每个违规的RuBOCOP COP名称.

    经过```--only-cops=``cops```将检查违规仅上市的红宝石`cops`,同时```--except-cops=``cops```将跳过检查列表`cops`. 任择`cops`应该是一个逗号分隔的COP名称列表.

    如果发现任何违反样式,则退出非零状态.

-   `switch` `formula` `version`SyLink所有特定的`version`属于`formula`安装到自制的前缀.

-   `tap`列出所有安装的水龙头.

-   `tap` [`--full`][`--force-auto-update`] ```user``/``repo``` [`URL`]点击配方库.

    用`URL`未指定的,使用HTTPS从GITHUB抽出公式库.由于在GITHUB上托管了这么多的抽头,所以这个命令是一个快捷方式.`tap`用户`/`回购协议`https://github.com/`用户`/homebrew-`回购协议.

    用`URL`指定的,使用任何传输协议从任意位置轻击公式库.`git`把手.一种论证形式`tap`简化,但也限制.这个双参数命令不作任何假设,因此可以从GitHub以外的地方克隆抽头,并使用HTTPS以外的协议,例如,SSH、GIT、HTTP、FTP(S)、RSYNC.

    默认情况下,存储库被克隆为浅拷贝.`--depth=1`),但如果`--full`通过,将使用完整的克隆.若要将浅拷贝转换为完整副本,则可以通过`--full`没有先打开.

    默认情况下,只有在GITHUB上托管的TAP才自动更新(出于性能原因).如果`--force-auto-update`通过,即使没有托管在GITHUB上,这个TAP也会自动更新.

    `tap`如果无事可做,则可重新运行并成功退出.然而,用不同的`URL`将导致异常,所以首先`untap`如果需要修改`URL`.

-   `tap` `--repair`从基于链表的基于目录的结构迁移抽取公式.

-   `tap` `--list-pinned`列出所有固定的水龙头.

-   `tap-info`显示所有安装的抽头的简要摘要.

-   `tap-info`(`--installed`γ`taps`):显示关于一个或多个的详细信息`taps`.

    通过`--installed`显示所有已安装的抽头的信息.

-   `tap-info` ```--json=``version```(`--installed`γ`taps`):打印一个JSON表示`taps`. 目前唯一接受的价值`version`是`v1`.

    通过`--installed`获取有关安装抽头的信息.

    有关使用JSON输出的示例,请参阅文档:[HTTPS://DOCS.BURW.S/QueReIn Burw](https://docs.brew.sh/Querying-Brew)

-   `tap-pin` `tap`针`tap`当公式名称由用户提供时,将其公式优先于核心.也见`tap-unpin`.

-   `tap-unpin` `tap`解开`tap`所以它的公式不再是优先的.也见`tap-pin`.

-   `uninstall`,`rm`,`remove` [`--force`][`--ignore-dependencies`] `formula`卸载`formula`.

    如果`--force`(或)`-f`通过,并且有多个版本`formula`安装,删除所有已安装的版本.

    如果`--ignore-dependencies`通过,卸载不会失败,即使公式取决于`formula`仍将安装.

-   `unlink` [`--dry-run`] `formula`删除链接`formula`从自制的前缀.这对于暂时禁用公式是有用的:`brew unlink`公式`&&`命令`&& brew link`公式

    如果`--dry-run`或`-n`通过,自制程序将列出所有未链接的文件,但实际上不会解开或删除任何文件.

-   `unpack` [`--git`γ`--patch`][`--destdir=``path`] `formulae`解压缩源文件`formulae`转换为当前工作目录的子目录.如果```--destdir=``path```给定子目录将在`path`相反.

    如果`--patch`通过,补丁`formulae`将应用于解压缩的源.

    如果`--git`(或)`-g`通过,将在解压缩的源中初始化Git存储库.这对于创建软件补丁非常有用.

-   `unpin` `formulae`解开`formulae`允许他们升级`brew upgrade`公式.也见`pin`.

-   `untap` `tap`删除一个轻敲的存储库.

-   `update` [`--merge`][`--force`]从GITHUB中获取最新版本的自制程序和所有公式`git`(1)执行任何必要的迁移.

    如果`--merge`然后指定`git merge`用于包括更新(而不是用于更新)`git rebase`)

    如果`--force`(或)`-f`如果不必要的话,那么总是要做一个较慢的、完全的更新检查.

-   `update-reset` [`repositories`]取回和重置自制程序和所有TAP存储库(或指定的)`repositories`使用`git`(1)最新`origin/master`. 注意,这将破坏所有未提交或提交的更改.

-   `upgrade` [`install-options`][`--cleanup`] [`--fetch-HEAD`][`--ignore-pinned`] [`--display-times`][`formulae`]升级过时的未经处理的啤酒(使用现有的安装选项).

    选项`install`命令在这里也是有效的.

    如果`--cleanup`指定或`HOMEBREW_UPGRADE_CLEANUP`然后设置升级的以前安装的版本`formulae`.

    如果`--fetch-HEAD`通过,获取上游存储库,以检测该公式的头安装是否过时.否则,当新的稳定版本或发布版本被释放时,将检查存储库的头部是否更新.

    如果`--ignore-pinned`通过,设置0退出代码,即使钉住公式没有升级.

    如果`--display-times`通过,在运行结束时打印每个公式的安装时间.

    如果`formulae`给出,只升级指定的啤酒(除非它们被钉住);`pin`,`unpin`)

-   `uses` [`--installed`][`--recursive`] [`--include-build`][`--include-test`] [`--include-optional`][`--skip-recommended`] [`--devel`|`--γ`HEAD] `formulae`显示指定的公式`formulae`作为依赖关系.当给出多个公式参数时,显示公式的相交.`formulae`.

    使用`--recursive`解析多个依赖级别.

    如果`--installed`通过,只列出安装公式.

    默认情况下,`uses`显示指定的所有公式`formulae`作为所需或推荐的依赖项.包括`:build`类型依赖性`--include-build`,包括`:test`类型依赖性`--include-test`并包括`:optional`依赖传递`--include-optional`. 跳过`:recommended`类型依赖性`--skip-recommended`.

    默认情况下,`uses`显示使用情况`formulae`通过稳定的构建.发现病例`formulae`用于开发或头部建立,通过`--devel`或`--HEAD`.

-   `--cache`显示自制程序的下载缓存.也见`HOMEBREW_CACHE`.

-   `--cache` [`--build-from-source`γ`-s`][`--force-bottle`] `formula`显示用于缓存的文件或目录`formula`.

-   `--cellar`展示自制的酒窖路径.*违约:* `$(brew --prefix)/Cellar`,或者如果该目录不存在,`$(brew --repository)/Cellar`.

-   `--cellar` `formula`显示地窖中的位置`formula`将不会安装任何版本的目录作为最后一个路径.

-   `--env` [`--shell=`(`shell`|`γ`)|`--auto`plain]将自制程序构建环境的概要作为一个简单的列表显示出来.

    通过```--shell=``shell```生成指定shell的环境变量列表,或`--shell=auto`检测当前外壳.

    如果命令的输出是通过管道发送的,并且没有指定shell,则将该列表格式化为导出.`bash`(1)除非`--plain`通过.

-   `--prefix`显示自制程序的安装路径.*违约:* `/usr/local`论MaOS与`/home/linuxbrew/.linuxbrew`Linux上

-   `--prefix` `formula`显示地窖中的位置`formula`是或将被安装.

-   `--repository`显示哪里是自制的`.git`目录位于.

-   `--repository` ```user``/``repo```显示龙头位置```user``/``repo```目录所在.

-   `--version`将自制程序的版本号打印到标准输出并退出.

## 开发者命令

-   `audit` [`--strict`][`--fix`] [`--online`][`--new-formula`] [`--display-cop-names`][`--display-filename`] [```--only=``method```γ```--except=``method```][`--only-cops=``cops`|`--except-cops=``cops`] [`formulae`]检查`formulae`针对自制代码风格的违规行为.这应该在提交一个新公式之前运行.

    如果没有`formulae`提供所有检查.

    如果`--strict`通过,额外的检查运行,包括Rubcopp风格检查.

    如果`--fix`通过,使用RuBOCCOP的自动纠正功能将自动修复样式违规.

    如果`--online`通过,需要运行网络连接的其他较慢的检查.

    如果`--new-formula`通过,检查新的公式是否符合自制程序的各种附加检查.这应该在创建新的公式和暗示时使用.`--strict`和`--online`.

    如果`--display-cop-names`通过,每个违章的RuBOCOP COP名称包含在输出中.

    如果`--display-filename`通过,每一行输出都带有被审核的文件或公式的名称前缀,以使输出易于GRIP.

    经过```--only=``method```只运行命名方法`audit_`方法,同时```--except=``method```将跳过命名方法`audit_`方法.任择`method`应该是逗号分隔的列表.

    经过```--only-cops=``cops```将检查违规仅上市的红宝石`cops`,同时```--except-cops=``cops```将跳过检查列表`cops`. 任择`cops`应该是一个逗号分隔的COP名称列表.

    `audit`如果发现任何错误,则退出非零状态.例如,这对于实现预提交钩子非常有用.

-   `bottle` [`--verbose`][`--no-rebuild`|`--keep-old`] [`--skip-relocation`][`--or-later`] [```--root-url=``URL```][`--force-core-tap`] [`--json`] `formulae`从安装的公式生成瓶子(二进制包)`--build-bottle`.

    如果公式指定了一个重建版本,它将在生成的DSL中递增.经过`--keep-old`将试图保持它的原始价值,而`--no-rebuild`将删除它.

    如果`--verbose`(或)`-v`通过,打印装瓶命令和遇到的任何警告.

    如果`--skip-relocation`通过,不要检查瓶子是否可以标记为可重新定位.

    如果`--root-url`通过,使用指定的`URL`作为瓶子的URL的根,而不是自制的默认值.

    如果`--or-later`通过,然后附加到瓶子标签上.

    如果`--force-core-tap`通过,甚至建造一个瓶子`formula`不是在家庭酿造/核心或任何安装抽头.

    如果`--json`通过,将瓶子信息写入JSON文件,可以用作`--merge`.

-   `bottle` `--merge` [`--keep-old`]`--write` [`--no-commit`]] `bottle_json_files`从一个瓶子中产生一个瓶子`--json`输出文件并打印合并到现有公式中的新DSL.

    如果`--write`通过,将更改写入公式文件.然后生成新的提交,除非`--no-commit`通过.

-   `bump-formula-pr` [`--devel`]`--dry-run` [`--write`]] [`--audit`γ`--strict`][`--mirror=``url`] [```--version=``version```][`--message=``message`](```--url=``URL``` ```--sha256=``sha-256```γ```--tag=``tag``` ```--revision=``revision```)`formula`创建一个拉请求,用一个新的URL或一个新的标签更新公式.

    如果A`URL`指定的`sha-256`还必须指定新下载的校验和.尽最大努力确定`sha-256`和`formula`如果用户没有提供一个或两个值,则将做出名称.

    如果A`tag`指定的Git提交`revision`还必须指定对应于该标签的内容.

    如果`--devel`通过,颠倒了发展,而不是稳定的版本.开发规范必须已经存在.

    如果`--dry-run`通过,打印将要做的事,而不是做.

    如果`--write`一起传递`--dry-run`执行一个不那么干燥的运行,使预期的文件修改,但不采取任何GIT行动.

    如果`--audit`通过,运行`brew audit`开学前的PR.

    如果`--strict`通过,运行`brew audit --strict`开学前的PR.

    如果```--mirror=``URL```传递,使用值作为镜像URL.

    如果```--version=``version```通过该值来重写从URL或标签中解析的值.注意`--version=0`可用于删除现有的`version`如果公式已经冗余,则从公式中重写.

    如果```--message=``message```通过,追加`message`默认的PR消息.

    如果`--no-browse`通过,不要通过`--browse`论证`hub`它在浏览器中打开拉取请求URL.相反,将其输出到命令行.

    如果`--quiet`通过,不要输出替换消息或警告重复的拉取请求.

    注意,此命令不能用于将公式从URL和sha256样式规范转换为标记和修订样式规范,反之亦然.它必须使用预先存在的公式已经使用的任何样式规范.

-   `create` `URL` [`--autotools`γ`--cmake`γ`--meson`][`--no-fetch`] [`--set-name` `name`][`--set-version` `version`] [`--tap` `user``/``repo`]生成可下载文件的公式`URL`并在编辑器中打开它.Homebrew将尝试自动派生公式名称和版本,但是如果失败,则必须创建自己的模板.这个`wget`公式作为一个简单的例子.对于完整的API有一个了解[HTTP://www. RuyDoc .iFo/GithBu/HubBurW/BurW/Mask/公式](http://www.rubydoc.info/github/Homebrew/brew/master/Formula).

    如果`--autotools`通过,为AutoTooCAD样式构建创建基本模板.如果`--cmake`通过,为CMAKE样式构建创建基本模板.如果`--meson`通过,创建介子样式构建的基本模板.

    如果`--no-fetch`通过,自制不会下载`URL`到缓存中,因此不会向您添加Sa256的公式.它也不会检查GITHUB API的GITHUB项目(填写描述和主页).

    选项`--set-name`和`--set-version`每一个都采用一个参数,并允许您显式地设置正在创建的包的名称和版本.

    选择权`--tap`以TAP作为参数,并在指定的TAP中生成公式.

-   `edit`打开所有自制程序进行编辑.

-   `edit` `formula`打开`formula`在编辑器中.

-   `extract` [`--force`] `formula` `tap` [`--version=``version`]查看仓库历史找到`version`属于`formula`并创建一个副本`tap`/公式/`formula`@`version`Rb.如果尚未安装TAP,则尝试在继续之前安装/克隆TAP.

    如果`--force`通过,目的地文件将被覆盖,如果它已经存在.否则,将保存现有文件.

    如果一个参数通过`--version`,`version`属于`formula`将提取并放置在目的地龙头中.否则,可以使用最新版本.

-   `formula` `formula`显示路径在哪里`formula`位于.

-   `irb` [`--examples`][`--pry`]进入交互式自制布鲁斯外壳.

    如果`--examples`通过,将显示几个例子.如果`--pry`通过或HOBBRWPRY PRY被设置,PRY将被用来代替IRB.

-   `linkage` [`--test`][`--reverse`] [`formulae`]检查安装公式的库链接.

    只适用于已安装的公式.如果在未安装的公式上运行,则会引发错误.

    如果`--test`通过,只显示缺少的库,如果发现任何缺少的库,则用非零退出代码退出.

    如果`--reverse`通过,打印DyLIB后面的二进制文件,链接到每个库的KEG引用.

    如果`formulae`给出,只针对指定的啤酒检查链接.

-   `man` [`--fail-if-changed`]生成自制程序的手册.

    如果`--fail-if-changed`如果在MangPad输出中检测到更改,则命令将返回失败状态代码.当MAPGE过时时,这可以用于通知CI.此外,新手册页中使用的日期将与现有手册页中使用的日期匹配(以允许在不考虑日期的情况下进行比较).

-   `prof` [`ruby options`]用Ruby探查器运行自制程序.例如:

-   `pull` [`--bottle`][`--bump`] [`--clean`][`--ignore-whitespace`] [`--resolve`][`--branch-okay`] [`--no-pbcopy`][`--no-publish`] [`--warn-on-publish-failure`][`--bintray-org=``bintray-org`] [`--test-bot-user=``test-bot-user`] `patch-source` [`patch-source`]\:

    从GITHUB提交或拉取请求中获取一个补丁,并将其应用于自制程序.可选地,安装由补丁改变的公式.

    各`patch-source`可能是:

    ~在自制/核心GITHUB存储库中的PR(拉请求)的ID号

    使用Github上的PR URL,使用网页或API URL格式.在这种形式下,PR可以在自制/酿造、自制/自制芯或任何龙头上.

    GITHUB上提交的URL

    "A"[http://詹金斯.](https://jenkins.brew.sh/job/...)"指定测试作业ID的字符串

    如果`--bottle`通过,处理瓶子,拉动瓶更新提交和发布文件Bintray.

    如果`--bump`通过一个公式PRS,自动重定向提交消息到我们的首选格式.

    如果`--clean`通过,不重写或以其他方式修改在拉扯PR.中发现的提交.

    如果`--ignore-whitespace`传递时,在应用差异时,静默地忽略空白差异.

    如果`--resolve`通过,当补丁无法应用时,请继续进行处理,允许用户解析,而不是中止.

    如果`--branch-okay`通过,不要警告,如果拉到一个分支除硕士(有用的测试).

    如果`--no-pbcopy`通过,不要复制任何东西到系统剪贴板.

    如果`--no-publish`通过,不要向Bintray公布瓶子.

    如果`--warn-on-publish-failure`通过了,如果在Bintray上出版瓶子失败了,请不要退出.

    如果```--bintray-org=``bintray-org```通过,在给定的BITCHORT组织发布.

    如果```--test-bot-user=``test-bot-user```通过,在GITHUB上从指定的用户拉动瓶子块提交.

-   `release-notes` [`--markdown`][`previous_tag`] [`end_ref`]在两个Git RIFS之间输出在自制/酿造中合并的拉取请求.如果没有`previous_tag`默认设置为最新标签.如果没有`end_ref`是否默认为`origin/master`.

    如果`--markdown`通过作为标记列表的输出.

-   `ruby` [`ruby options`]运行一个Ruby实例,加载的是自制程序的库.例如:

-   `tap-new` ```user``/``repo```:为新的TAP生成模板文件.

-   `test` [`--devel`γ`--HEAD`][`--debug`] [`--keep-tmp`] `formula`大多数公式提供了一种测试方法.`brew test` `formula`运行这个测试方法.没有标准的输出或返回代码,但是通常应该向用户指示安装的公式是否出错.

    要测试公式的开发或头版本,请使用`--devel`或`--HEAD`.

    如果`--debug`(或)`-d`通过测试失败,将启动交互式调试器,访问临时测试目录中的IRB或shell.

    如果`--keep-tmp`通过,为测试创建的临时文件不会被删除.

    例子:`brew install jruby && brew test jruby`

-   `tests` [`--verbose`][`--coverage`] [`--generic`][`--no-compat`] [```--only=``test_script```\[```:``line_number```\]][`--seed=``seed`] [`--online`][`--official-cmd-taps`]运行HunBurw的单元和集成测试.如果提供,```--only=``test_script```只运行`test_script`R.SP.RB,以及`--seed`用所提供的值而不是随机的种子随机化测试.

    如果`--verbose`(或)`-v`通过,打印运行测试的命令.

    如果`--coverage`通过,也生成代码覆盖报告.

    如果`--generic`通过,只运行OS不可知的测试.

    如果`--no-compat`通过,在运行测试时不要加载兼容层.

    如果`--online`通过测试,包括使用GITHUB API的测试和使用任何TAP用于官方外部命令的测试.

-   `update-test` [```--commit=``commit```][`--before=``date`] [`--to-tag`][`--keep-tmp`]运行测试`brew update`使用新的存储库克隆.

    如果没有参数传递,则使用`origin/master`作为开始提交.

    如果```--commit=``commit```通过,使用`commit`作为开始提交.

    如果```--before=``date```通过,使用提交`date`作为开始提交.

    如果`--to-tag`通过,设置`HOMEBREW_UPDATE_TO_TAG`测试标签之间的更新.

    如果`--keep-tmp`通过,保留包含新存储库克隆的临时目录.

## 官方外部命令

-   `bundle` `command`:

    Buffer-Runby对来自家庭自制的非Ruby依赖性.


```
  `bundle` [`install`] [`-v`|`--verbose`] [`--no-upgrade`] [`--file=``path`|`--global`]:

  Install or upgrade all dependencies in a Brewfile.



  `brew bundle dump` [`--force`] [`--describe`] [`--file=``path`|`--global`]

  Write all installed casks/formulae/taps into a Brewfile.



  `brew bundle cleanup` [`--force`] [`--zap`] [`--file=``path`|`--global`]

  Uninstall all dependencies not listed in a Brewfile.



  `brew bundle check` [`--no-upgrade`] [`--file`=`path`|`--global`] [`--verbose`]

  Check if all dependencies are installed in a Brewfile. Missing dependencies are listed in verbose mode. `check` will exit on the first category missing a dependency unless in verbose mode.



  `brew bundle exec` `command`

  Run an external command in an isolated build environment.



  `brew bundle list` [`--all`|`--brews`|`--casks`|`--taps`|`--mas`] [`--file=``path`|`--global`]

  List all dependencies present in a Brewfile, optionally limiting by types.

  By default, only brew dependencies are output.



  If `-v` or `--verbose` are passed, print verbose output.



  If `--no-upgrade` is passed, don't run `brew upgrade` outdated dependencies.

  Note they may still be upgraded by `brew install` if needed.



  If `--force` is passed, uninstall dependencies or overwrite an existing Brewfile.



  If `--zap` is passed, casks will be removed using the `zap` command instead of `uninstall`.



  If `--file=`path is passed, the Brewfile path is set accordingly

  Use `--file=-` to output to console.



  If `--global` is passed, set Brewfile path to `$HOME/.Brewfile`.



  If `--describe` is passed, output a description comment above each line.

  This comment will not be output if the dependency does not have a description.



  If `-h` or `--help` are passed, print this help message and exit.
```

自制/自制包[HTTPS://GITHUBCOM/HOBRWW/HOBBRWW-束](https://github.com/Homebrew/homebrew-bundle)

-   `cask` [`--version`γ|audit`γ`cat|γ`cleanup`γ|create`γ`doctor|γ`edit`γ|fetch`γ`home|γ`info`]安装MaOS应用程序作为二进制文件分发.

自制/自制桶[HTTPS://GITHUBCOM/HOMEBWW/HOMEBWW-CKASE](https://github.com/Homebrew/homebrew-cask)

-   `services` `command`:

    将自制公式与MaOSOS集成`launchctl`经理.


```
  [`sudo`] `brew services list`

  List all running services for the current user (or `root`)



  [`sudo`] `brew services run` `formula|--all`

  Run the service `formula` without starting at login (or boot).



  [`sudo`] `brew services` `start` `formula|--all`

  Start the service `formula` immediately and register it to launch at login (or `boot`).



  [`sudo`] `brew services` `stop` `formula|--all`

  Stop the service `formula` immediately and unregister it from launching at login (or `boot`).



  [`sudo`] `brew services` `restart` `formula|--all`

  Stop (if necessary) and start the service immediately and register it to launch at login (or `boot`).



  [`sudo`] `brew services` `cleanup`

  Remove all unused services.



  If `sudo` is passed, operate on `/Library/LaunchDaemons` (started at boot).

  Otherwise, operate on `~/Library/LaunchAgents (started at login)`.
```

自制/自制服务[HTTPS://GITHUBCOM/HOMEBWW/HOMEBRW-Services](https://github.com/Homebrew/homebrew-services)

## 自定义外部命令

自制饮料`git`(1)支持外部命令.这些是驻留在某处的可执行脚本.`PATH`命名```brew-``cmdname```或```brew-``cmdname``.rb```,可以这样调用`brew` `cmdname`. 这允许您创建自己的命令而不修改HOBBURW的内部结构.

在文档中可以找到创建自己命令的指令:[HTTPS://DOCS.BURW.S/外部命令](https://docs.brew.sh/External-Commands)

## 指定公式

许多自制命令接受一个或多个`formula`争论.这些论点可以采取几种不同的形式:

-   公式的名称:`git`,`node`,`wget`.

-   抽头公式的完全限定名称:有时来自轻敲存储库的公式可能与`homebrew/core`. 你仍然可以通过使用特殊的语法来访问这些公式.`homebrew/dupes/vim`或`homebrew/versions/node4`.

-   任意URL:自制程序可以通过URL安装公式,例如`https://raw.github.com/Homebrew/homebrew-core/master/Formula/git.rb`. 公式文件将被缓存以供以后使用.

## 环境

注意环境变量必须有一个待检测的值.例如,`export HOMEBREW_NO_INSECURE_REDIRECT=1`而不仅仅是`export HOMEBREW_NO_INSECURE_REDIRECT`.

-   `HOMEBREW_ARTIFACT_DOMAIN`如果设置,则指示自制程序用这个变量前缀所有下载URL,包括那些用于瓶子的下载URL.例如,一个带有URL的公式`https://example.com/foo.tar.gz`但是`HOMEBREW_ARTIFACT_DOMAIN=http://localhost:8080`将从`http://localhost:8080/example.com/foo.tar.gz`.

-   `HOMEBREW_AUTO_UPDATE_SECS`如果设置,自制将只检查自动约会一次每秒的时间间隔.

    *违约:* `60`.

-   `HOMEBREW_AWS_ACCESS_KEY_ID`,`HOMEBREW_AWS_SECRET_ACCESS_KEY`当使用`S3`下载策略,HOBBURW将在这些变量中查找访问凭据(参见[http://DOCS.AWS.Amazon .COM/CLI/最新/用户指南/CLI CHAP启动.](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-environment)从AWS检索这些访问凭据.如果没有设置,`S3`下载策略将以公共(无符号)URL下载.

-   `HOMEBREW_BOTTLE_DOMAIN`默认情况下,自制程序使用`https://homebrew.bintray.com/`作为瓶子的下载镜.如果设置,指示自制,而不是使用给定的URL.例如,`HOMEBREW_BOTTLE_DOMAIN=http://localhost:8080`将导致所有瓶子从前缀下载`http://localhost:8080/`.

-   `HOMEBREW_BROWSER`如果是SET,在打开项目主页时使用这个设置作为浏览器,而不是OS默认浏览器.

-   `HOMEBREW_BUILD_FROM_SOURCE`如果设置的话,即使公式提供瓶子,也要指示自制程序从源头编译.此环境变量旨在由自制程序开发人员使用.使用此环境变量时,如果遇到错误,请不要提交文件.

-   `HOMEBREW_CACHE`如果设置,指示自制程序使用给定的目录作为下载缓存.

    *违约:* `~/Library/Caches/Homebrew`.

-   `HOMEBREW_CURLRC`如果设置,自制不会通过`-q`调用时`curl`(1)禁止使用`curlrc`)

-   `HOMEBREW_CURL_VERBOSE`如果设置,自制将通过`--verbose`调用时`curl`(1).

-   `HOMEBREW_DEBUG`如果设置,任何可以发出调试信息的命令都会这样做.

-   `HOMEBREW_DEBUG_INSTALL`什么时候`brew install -d`或`brew install -i`掉进一个壳里,`HOMEBREW_DEBUG_INSTALL`将被设置为正在酝酿的公式的名称.

-   `HOMEBREW_DEBUG_PREFIX`什么时候`brew install -d`或`brew install -i`掉进一个壳里,`HOMEBREW_DEBUG_PREFIX`将被设置为正在酝酿的公式的地窖中的目标前缀.

-   `HOMEBREW_DEVELOPER`如果设置了,Homebrew将调整行为,使其与Homebrew开发人员(活动或萌芽)更加相关,例如将警告转换为错误.

-   `HOMEBREW_EDITOR`如果设置,自制程序将在编辑单个公式时使用此编辑器,或在同一目录中使用多个公式.

    *注:* `brew edit`将打开所有的自制文件作为不连续的文件和目录.在项目模式下,TeTeMax可以正确处理,但许多编辑器在这种情况下会做一些奇怪的事情.

-   `HOMEBREW_FORCE_BREWED_CURL`如果设置,自制将使用自制的安装`curl`而不是系统版本.

-   `HOMEBREW_FORCE_VENDOR_RUBY`如果设置的话,即使Ruby的系统版本足够新,HoubBurw也会使用它的版本,可重新定位的Ruby版本.

-   `HOMEBREW_GIT`当使用Git时,自制程序将使用`GIT`如果设置,自制程序如果安装了Git,或者系统提供二进制.

    将此设置为强制自制程序使用特定的Git二进制.

-   `HOMEBREW_FORCE_BREWED_GIT`如果设置,自制将使用自制的安装`git`而不是系统版本.

-   `HOMEBREW_GITHUB_API_TOKEN`GITHUB API的个人访问令牌,您可以在其上创建[HTTPS://GITHUB.COM/STATIONS/ToKEN](https://github.com/settings/tokens). 如果设置,GITHUB将允许更多的API请求.见[http://Dealth.GITHUB.COM/V3/Y速率限制](https://developer.github.com/v3/#rate-limiting)欲了解更多信息.HOMBURW使用GITHUB API的特性,例如`brew search`.

    *注:*自制程序不需要任何范围的权限.

-   `HOMEBREW_INSTALL_BADGE`在每个成功构建的安装概要之前打印的文本.默认为啤酒表情.

-   `HOMEBREW_LOGS`如果设置,自制程序将使用给定的目录来存储日志文件.

-   `HOMEBREW_MAKE_JOBS`如果设置,指示自制程序使用的值`HOMEBREW_MAKE_JOBS`作为并行作业运行时的数量`make`(1).

    *违约:*可用的CPU核数.

-   `HOMEBREW_NO_ANALYTICS`如果设置,自制不会发送分析.见:[HTTPS://DOCS.BURW.SH/分析](https://docs.brew.sh/Analytics)

-   `HOMEBREW_NO_AUTO_UPDATE`如果设置,自制程序在运行前不会自动更新.`brew install`,`brew upgrade`或`brew tap`.

-   `HOMEBREW_NO_COLOR`如果设置,自制不会打印文字加上颜色.

-   `HOMEBREW_NO_EMOJI`如果设置,自制不会打印`HOMEBREW_INSTALL_BADGE`一个成功的建筑.

    *注:*HOBBURW将只尝试打印狮子或更新的表情符号.

-   `HOMEBREW_NO_INSECURE_REDIRECT`如果设置,自制程序将不允许从安全的HTTPS重定向到不安全的HTTP.

    虽然确保您的下载是完全安全的,但这可能导致源SourceForge、一些基于GNU和GNOME的公式无法下载.

-   `HOMEBREW_NO_GITHUB_API`如果设置,自制程序将不使用GITHUB API进行E.G搜索或在失败的安装上获取相关的问题.

-   `HOMEBREW_PRY`如果设置,自制将使用`pry`对于`brew irb`命令.

-   `HOMEBREW_SVN`当从颠覆出口时,自制将使用`HOMEBREW_SVN`如果设置,自制的子版本如果安装,或者系统提供二进制.

    设置这迫使自制程序使用特定的`svn`二元的.

-   `HOMEBREW_TEMP`如果设置,指示自制使用`HOMEBREW_TEMP`作为构建包的临时目录.如果您的系统临时目录和Homebrew Prefix位于不同的卷上,那么这可能是需要的,因为当目标还不存在时,macOS很难跨卷移动符号链接.

    这个问题通常发生在使用FielvaUT或自定义SSD配置时.

-   `HOMEBREW_UPGRADE_CLEANUP`如果设置,`brew upgrade`总是假设`--cleanup`已经通过了.

-   `HOMEBREW_VERBOSE`如果设置,自制总是假设`--verbose`运行命令时.

-   `http_proxy`设置要使用的HTTP代理`curl`,`git`和`svn`当通过自制软件下载时.

-   `https_proxy`设置要使用的HTTPS代理`curl`,`git`和`svn`当通过自制软件下载时.

-   `all_proxy`设置SoCKS5代理`curl`,`git`和`svn`当通过自制软件下载时.

-   `ftp_proxy`设置要使用的FTP代理`curl`,`git`和`svn`当通过自制软件下载时.

-   `no_proxy`设置逗号分隔的主机名和域名,这些列表应被排除在代理之外.`curl`,`git`和`svn`当通过自制软件下载时.

## 在代理背后使用自制软件

使用`http_proxy`,`https_proxy`,`all_proxy`,`no_proxy`和/或`ftp_proxy`以上记录.

例如,对于未经验证的HTTP或SoCKS5代理:

```
export http_proxy=http://`host`:`port`

export all_proxy=socks5://`host`:`port`
```

以及用于身份验证的HTTP代理:

```
export http_proxy=http://`user`:`password`@`host`:`port`
```

## 也见

自制文件:[HTTPS://DOCS.BurW.SH](https://docs.brew.sh)

`brew-cask`(1)`git`(1)`git-log`(1)

## 作者

自制啤酒的主要维护者是Mike McQuaid.

HutBurw的项目领导委员会是Mike McQuaid、JCeo、Misty De Meo和Markus Reiter.

"自制/酿造"目前其他的维护者有克劳迪娅、米奇卡·波普夫、肖恩·杰克曼、朱崇宇、共产主义者、维特·加尔沃、JCount、米蒂·德·梅奥、高瑟姆·古利、马库斯·赖特、史蒂文·彼得斯、张乔纳森·伍德拉夫.

HOBREW/BREW的Linux支持(和Linuxbrew)维护者是Michka Popoff和Shaun Jackman.

"自制/自制-核心"的其他现有维护者有克劳迪娅、米奇卡·波普夫、肖恩·杰克曼、朱崇宇、公社、伊扎克·比克曼、肖恩·莫雷纳、简·维尔贾宁、维克多·斯扎卡茨、FX考德特、史蒂文·彼得斯、JCount、米蒂·德梅奥和汤姆·斯昆詹斯.

前维系者包括多明尼克·蒂勒、蒂姆·史密斯、巴普蒂斯特·方丹、徐成、马丁·阿法纳斯犹太人、布雷特·科昂、查理·夏普斯丁、杰克·纳格尔、亚当·范登堡、安德鲁·扬克、亚历克斯·邓恩、中立科、托马斯·帕乔、乌拉兹斯拉夫·沙布林斯基、艾丽莎·罗斯、伊洛维兹夫斯和霍梅布尔.EW的创造者:Max Howell.

## 漏洞

看我们在Github上的问题:

-   自制/酿造[HTTPS://GITHUB/COM/HOBRWW/BRW/问题](https://github.com/Homebrew/brew/issues)

-   自制/自制核心[HTTPS://GITHUBCOM/HOBRWW/HOMEBWW-CORE/发行](https://github.com/Homebrew/homebrew-core/issues)

[synopsis]: #SYNOPSIS "SYNOPSIS"

[description]: #DESCRIPTION "DESCRIPTION"

[essential commands]: #ESSENTIAL-COMMANDS "ESSENTIAL COMMANDS"

[commands]: #COMMANDS "COMMANDS"

[developer commands]: #DEVELOPER-COMMANDS "DEVELOPER COMMANDS"

[official external commands]: #OFFICIAL-EXTERNAL-COMMANDS "OFFICIAL EXTERNAL COMMANDS"

[custom external commands]: #CUSTOM-EXTERNAL-COMMANDS "CUSTOM EXTERNAL COMMANDS"

[specifying formulae]: #SPECIFYING-FORMULAE "SPECIFYING FORMULAE"

[environment]: #ENVIRONMENT "ENVIRONMENT"

[using homebrew behind a proxy]: #USING-HOMEBREW-BEHIND-A-PROXY "USING HOMEBREW BEHIND A PROXY"

[see also]: #SEE-ALSO "SEE ALSO"

[authors]: #AUTHORS "AUTHORS"

[bugs]: #BUGS "BUGS"

[-]: -.html
